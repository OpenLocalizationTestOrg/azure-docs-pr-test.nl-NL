---
title: aaaManage Azure Key Vault met CLI | Microsoft Docs
description: Gebruik van deze zelfstudie tooautomate algemene taken in de Sleutelkluis via Hallo CLI 2.0
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: ambapat
ms.openlocfilehash: 76855c0ea09b6b307159468382a6a63627205556
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-key-vault-using-cli-20"></a>Beheren met CLI 2.0 Sleutelkluis
Azure Sleutelkluis is beschikbaar in de meeste regio's. Zie voor meer informatie, Hallo [pagina prijzen van Sleutelkluis](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Inleiding
Gebruik van deze zelfstudie toohelp die u aan de slag met Azure Key Vault toocreate een geharde container (een kluis) in Azure, toostore en beheren van de cryptografische sleutels en geheimen in Azure. Deze begeleidt u bij Hallo proces van het gebruik van Azure platformoverschrijdende opdrachtregelinterface toocreate een kluis die een sleutel of het wachtwoord dat u vervolgens met een Azure-toepassing gebruiken kunt bevat. Deze vervolgens ziet u hoe een toepassing kunt vervolgens sleutel of het wachtwoord.

**Geschatte tijd toocomplete:** 20 minuten

> [!NOTE]
> Deze zelfstudie bevat geen instructies over hoe toowrite hello Azure-toepassing met een van de stappen hello, waaruit blijkt hoe tooauthorize een toouse toepassing een sleutel of geheim in de sleutel Hallo-kluis.
>
> Deze zelfstudie maakt gebruik van Hallo nieuwste Azure CLI 2.0.
>
>

Zie [Wat is Azure Sleutelkluis?](key-vault-whatis.md) voor algemene informatie over Azure Sleutelkluis.

## <a name="prerequisites"></a>Vereisten
toocomplete in deze zelfstudie hebt u hello te volgen:

* Een abonnement tooMicrosoft Azure. Als u geen abonnement hebt, kunt u zich aanmelden voor een [gratis proefversie](https://azure.microsoft.com/pricing/free-trial).
* Opdrachtregelinterface versie 2.0 of hoger. tooinstall Hallo meest recente versie en verbinding maken met tooyour Azure-abonnement, Zie [installeren en configureren van hello Azure platformoverschrijdende opdrachtregelinterface 2.0](/cli/azure/install-azure-cli).
* Een toepassing die worden zal geconfigureerde toouse Hallo sleutel of het wachtwoord die u in deze zelfstudie maakt. Er is een voorbeeldtoepassing beschikbaar is via Hallo [Microsoft Download Center](http://www.microsoft.com/download/details.aspx?id=45343). Zie voor instructies Hallo bijbehorende Leesmij-bestand.

## <a name="getting-help-with-azure-cross-platform-command-line-interface"></a>Help-informatie met Azure platformoverschrijdende opdrachtregelinterface
Deze zelfstudie wordt ervan uitgegaan dat u bekend met Hallo-opdrachtregelinterface (Bash, Terminal-opdrachtprompt bent)

Hallo--help- of -h parameter is tooview help gebruikt voor specifieke opdrachten. U kunt ook Hallo hello azure help [opdracht] [opties] indeling kan ook worden gebruikt tooreturn dezelfde informatie. Bijvoorbeeld Hallo volgende alle return opdrachten Hallo dezelfde informatie:

```
az account set --help
az account set -h
```

Raadpleeg bij twijfel over Hallo parameters nodig is voor een opdracht met behulp van toohelp--help, -h of az help [opdracht].

U kunt ook de volgende zelfstudies tooget bekend met Azure Resource Manager in Azure platformoverschrijdende opdrachtregelinterface Hallo lezen:

* [Azure CLI installeren](/cli/azure/install-azure-cli)
* [Aan de slag met Azure CLI 2.0](/cli/azure/get-started-with-azure-cli)

## <a name="connect-tooyour-subscriptions"></a>Verbinding maken met tooyour abonnementen
toolog aan met een organisatieaccount, gebruik Hallo volgende opdracht:

```
az login -u username@domain.com -p password
```

of als u toolog wilt in interactief typen

```
az login
```

Als u meerdere abonnementen hebt en wilt dat een specifieke één toouse toospecify voor Azure Sleutelkluis, typt u Hallo toosee Hallo abonnementen voor uw account te volgen:

```
az account list
```

Vervolgens toospecify Hallo abonnement toouse, type:

```
az account set --subscription <subscription name or ID>
```

Zie voor meer informatie over het configureren van Azure platformoverschrijdende opdrachtregelinterface [Azure CLI installeren](/cli/azure/install-azure-cli).

## <a name="create-a-new-resource-group"></a>Een nieuwe resourcegroep maken
Wanneer u Azure Resource Manager gebruikt, worden alle gerelateerde resources gemaakt binnen een resourcegroep. We gaan een nieuwe resourcegroep 'ContosoResourceGroup' maken voor deze zelfstudie.

```
az group create -n 'ContosoResourceGroup' -l 'East Asia'
```

Hallo eerste parameter is de naam van resourcegroep en de tweede parameter Hallo Hallo locatie. Voor de locatie, gebruikt u Hallo opdracht `az account list-locations` tooidentify hoe toospecify een alternatieve locatie toohello een in dit voorbeeld. Als u meer informatie nodig hebt, typt: `az account list-locations -h`.

## <a name="register-hello-key-vault-resource-provider"></a>De registerbronprovider hello Sleutelkluis
Zorg ervoor dat Sleutelkluis-resourceprovider is geregistreerd in uw abonnement:

```
az provider register -n Microsoft.KeyVault
```

Dit moet alleen toobe gebeurt eenmaal per abonnement.

## <a name="create-a-key-vault"></a>Een sleutelkluis maken
Gebruik Hallo `az keyvault create` opdracht toocreate een sleutelkluis. Dit script heeft drie verplichte parameters: de naam van een resource-groep, een sleutelkluisnaam en Hallo geografische locatie.

Bijvoorbeeld, als u Hallo kluisnaam ContosoKeyVault, Hallo Resourcegroepnaam ContosoResourceGroup en Hallo-locatie van Oost-Azië, typt u:
```
az keyvault create --name 'ContosoKeyVault' --resource-group 'ContosoResourceGroup' --location 'East Asia'
```

Hallo-uitvoer van deze opdracht worden de eigenschappen van Hallo sleutelkluis die u zojuist hebt gemaakt. Hallo twee belangrijkste eigenschappen zijn:

* **naam**: In Hallo voorbeeld is dit ContosoKeyVault. U gebruikt deze naam voor andere Sleutelkluis-opdrachten.
* **vaultUri**: In Hallo voorbeeld is dit https://contosokeyvault.vault.azure.net. Toepassingen die via de REST API gebruikmaken van uw kluis, moeten deze URI gebruiken.

Uw Azure-account is nu geautoriseerde tooperform bewerkingen op deze sleutel kluis. Tot dusver is er nog niemand anders gemachtigd.

## <a name="add-a-key-or-secret-toohello-key-vault"></a>Een sleutel of geheim toohello sleutelkluis toevoegen
Als u toocreate Azure Sleutelkluis een softwarematig beveiligde sleutel voor u wilt, gebruikt u Hallo `az key create` opdracht in en typt u de volgende Hallo:
```
az keyvault key create --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --protection software
```
Als u een bestaande sleutel in een .pem-bestand opgeslagen als een lokaal bestand in een bestand met de naam die u wilt dat tooupload tooAzure Sleutelkluis softkey.pem hebt, typt u na het tooimport Hallo sleutel uit Hallo Hallo. PEM-bestand, dat Hallo sleutel met software in Hallo Sleutelkluis-service beveiligt kan worden gebruikt:
```
az keyvault key import --vault-name 'ContosoKeyVault' --name 'ContosoFirstKey' --pem-file './softkey.pem' --pem-password 'PaSSWORD' --protection software
```
U kunt nu naar Hallo sleutel dat u hebt gemaakt of geüpload tooAzure Sleutelkluis, met behulp van de URI verwijzen. Gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey** tooalways halen van de huidige versie Hallo en gebruik **https://ContosoKeyVault.vault.azure.net/keys/ContosoFirstKey/ cgacf4f763ar42ffb0a1gca546aygd87** tooget deze specifieke versie.

tooadd een kluis geheime toohello, die een wachtwoord met de naam SQLPassword en die Hallo-waarde van Pa$ $w0rd tooAzure Sleutelkluis, type hello te volgen:
```
az keyvault secret set --vault-name 'ContosoKeyVault' --name 'SQLPassword' --value 'Pa$$w0rd'
```
U kunt nu verwijzen naar dit wachtwoord dat u met behulp van de URI tooAzure Sleutelkluis, toegevoegd. Gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword** tooalways halen van de huidige versie Hallo en gebruik **https://ContosoVault.vault.azure.net/secrets/SQLPassword/ 90018dbb96a84117a0d2847ef8e7189d** tooget deze specifieke versie.

We bekijken Hallo sleutel of geheim dat u zojuist hebt gemaakt:

* tooview uw sleutel, type:`az keyvault key list --vault-name 'ContosoKeyVault'`
* tooview uw geheime, type:`az keyvault secret list --vault-name 'ContosoKeyVault'`

## <a name="register-an-application-with-azure-active-directory"></a>Een toepassing registreren met Azure Active Directory
Deze stap wordt doorgaans uitgevoerd door een ontwikkelaar op een afzonderlijke computer. Er is geen specifieke tooAzure Sleutelkluis maar opgenomen, voor de volledigheid.

> [!IMPORTANT]
> toocomplete hello zelfstudie, uw account, Hallo kluis en Hallo-toepassing die u in deze stap registreren wilt moeten alle liggen Hallo dezelfde Azure-directory.
>
>

Toepassingen die gebruikmaken van een sleutelkluis moeten een token van Azure Active Directory gebruiken om zich te verifiëren. toodo deze, Hallo eigenaar van de toepassing hello moet Hallo-toepassing eerst registreren in Azure Active Directory. De eigenaar van de toepassing hello opgehaald Hallo na registratie Hallo volgende waarden:

* Een **toepassings-ID** (ook wel bekend als een Client-ID) en **verificatiesleutel** (ook wel bekend als Hallo gedeelde geheim genoemd). Hallo-toepassing moet aanwezig zijn beide van deze waarden tooAzure Active Directory, tooget een token. Hoe de toepassing hello is dit afhankelijk van de toepassing hello toodo geconfigureerd. Voor Hallo voorbeeldtoepassing voor Sleutelkluis stelt u de eigenaar van de toepassing hello deze waarden in Hallo app.config-bestand.

tooregister hello toepassing in Azure Active Directory:

1. Meld u aan toohello Azure-portal.
2. Klik aan de linkerkant Hallo op **Azure Active Directory**, en selecteer vervolgens Hallo directory waarin u uw toepassing wilt registreren. <br> <br> 

> [!Note] 
> Hallo moet u dezelfde map waarin zich hello Azure-abonnement waarmee u de sleutelkluis hebt gemaakt. Als u niet welke directory dit weet is, klikt u op **instellingen**, identificeert Hallo-abonnement waarmee u de sleutelkluis hebt gemaakt en Opmerking Hallo-naam van Hallo-map weergegeven in de laatste kolom Hallo.

3. Klik op **TOEPASSINGEN**. Als u geen apps tooyour directory zijn toegevoegd, ziet deze pagina alleen Hallo **een App toevoegen** koppeling. Klik op de koppeling Hallo of, u kunt ook klikken op Hallo **toevoegen** op Hallo opdrachtbalk klikken.
4. In Hallo **toepassing toevoegen** wizard op Hallo **wat wilt u wilt dat toodo?** pagina, klikt u op **mijn organisatie ontwikkelt toepassing toevoegen**.
5. Op Hallo **Vertel ons over uw toepassing** pagina, Geef een naam voor uw toepassing en selecteer **WEBTOEPASSING en/of WEB-API** (Hallo standaard). Klik op volgende Hallo-pictogram.
6. Op Hallo **App-eigenschappen** pagina, geeft u Hallo **AANMELDINGS-URL** en **APP ID URI** voor uw webtoepassing. Als uw toepassing deze waarden niet heeft, kunt u voor deze stap zelf iets verzinnen (u kunt voor beide vakken bijvoorbeeld http://test1.contoso.com opgeven). Het maakt niet uit als deze sites bestaan; Wat is het belangrijk is dat die Hallo app ID URI voor elke toepassing verschilt voor elke toepassing in uw directory. Hallo directory gebruikt deze tekenreeks tooidentify uw app.
7. Klik op Hallo voltooid pictogram toosave uw wijzigingen in de wizard Hallo.
8. Klik op de pagina snel starten Hallo **configureren**.
9. Schuif toohello **sleutels** sectie, selecteer Hallo duur en klik vervolgens op **opslaan**. Hallo-pagina wordt vernieuwd en bevat nu een sleutelwaarde. U moet uw toepassing configureren met deze sleutelwaarde en Hallo **CLIENT-ID** waarde. (Instructies voor deze configuratie zijn toepassingsspecifiek.)
10. Kopieer Hallo client-id-waarde van deze pagina wordt gebruikt in Hallo volgende stap tooset machtigingen voor uw kluis.

## <a name="authorize-hello-application-toouse-hello-key-or-secret"></a>Autoriseren hello toepassing toouse Hallo sleutel of geheim
tooauthorize hello toepassing tooaccess Hallo sleutel of geheim in Hallo kluis, gebruik Hallo `az keyvault set-policy` opdracht.

Bijvoorbeeld, als de kluisnaam van uw ContosoKeyVault en Hallo toepassing die u wilt dat tooauthorize client-ID van 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed heeft en u wilt dat tooauthorize Hallo toepassing toodecrypt en meld u met sleutels in uw kluis, voert Hallo te volgen:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --key-permissions decrypt sign
```

Als u dat dezelfde toepassing tooread geheimen tooauthorize in uw kluis wilt, voert u Hallo volgende:
```
az keyvault set-policy --name 'ContosoKeyVault' --spn 8f8c4bbd-485b-45fd-98f7-ec6300b7b4ed --secret-permissions get
```
## <a name="if-you-want-toouse-a-hardware-security-module-hsm"></a>Als u wilt dat toouse een hardware security module (HSM)
U kunt voor de zekerheid importeren of genereren van sleutels in hardware security modules (HSM's) die Hallo HSM-grens nooit verlaten. Hallo HSM's zijn FIPS 140-2 Level 2-gevalideerde modules. Als deze vereiste niet van toepassing tooyou, kunt u deze sectie overslaan en gaat u te[hello sleutelkluis en de bijbehorende sleutels en geheimen verwijderen](#delete-the-key-vault-and-associated-keys-and-secrets).

toocreate deze met HSM beveiligde sleutels, moet u een kluis abonnement die ondersteuning biedt voor met HSM beveiligde sleutels hebben.

Wanneer u Hallo keyvault maakt, voegt u de parameter 'sku' hello:

```
az keyvault create --name 'ContosoKeyVaultHSM' --resource-group 'ContosoResourceGroup' --location 'East Asia' --sku 'Premium'
```
U kunt softwarematige beveiligde sleutels toevoegen (zoals eerder is weergegeven) en de HSM beveiligde sleutels toothis-kluis. toocreate een HSM beschermde sleutel set Hallo bestemming parameter too'HSM':

```
az keyvault key create --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --protection 'hsm'
```

U kunt volgende opdracht tooimport een sleutel uit een .pem-bestand op uw computer hello gebruiken. Deze opdracht wordt Hallo sleutel geïmporteerd in HSM's in Hallo Sleutelkluis-service:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --pem-file '/.softkey.pem' --protection 'hsm' --pem-password 'PaSSWORD'
```
de volgende opdracht Hallo importeert u een 'bring your own key' (BYOK)-pakket. Hiermee kunt u uw sleutel in uw lokale HSM genereren en overdragen tooHSMs in Hallo Sleutelkluis-service, zonder Hallo sleutel Hallo HSM-grens verlaat:

```
az keyvault key import --vault-name 'ContosoKeyVaultHSM' --name 'ContosoFirstHSMKey' --byok-file './ITByok.byok' --protection 'hsm'
```
Voor instructies over het gedetailleerde toogenerate dit BYOK-pakket Zie [hoe toouse HSM-Protected sleutels met Azure Sleutelkluis](key-vault-hsm-protected-keys.md).

## <a name="delete-hello-key-vault-and-associated-keys-and-secrets"></a>Hallo sleutelkluis en de bijbehorende sleutels en geheimen verwijderen
Als u niet langer Hallo sleutelkluis en sleutel Hallo of het geheim die deze bevat, kunt u Hallo sleutelkluis verwijderen met behulp van Hallo `az keyvault delete` opdracht:

```
az keyvault delete --name 'ContosoKeyVault'
```

Of u kunt een volledige Azure-resourcegroep, waaronder Hallo sleutelkluis en alle andere resources die u hebt opgenomen in de groep verwijderen:

```
az group delete --name 'ContosoResourceGroup'
```

## <a name="other-azure-cross-platform-command-line-interface-commands"></a>Andere opdrachten Azure platformoverschrijdende opdrachtregelinterface
Andere opdrachten die u wellicht nuttig voor het beheer van Azure Sleutelkluis.

Met deze opdracht worden alle sleutels en geselecteerde eigenschappen weergegeven in een tabel:

AZ keyvault sleutellijst--naam sleutelkluis 'ContosoKeyVault'

Deze opdracht wordt een volledige lijst met eigenschappen voor de opgegeven sleutel Hallo weergegeven:

AZ keyvault sleutel weergeven--kluisnaam ContosoKeyVault--de naam 'ContosoFirstKey'

Met deze opdracht worden alle geheime namen en geselecteerde eigenschappen weergegeven in een tabel:

AZ keyvault geheime lijst--naam sleutelkluis 'ContosoKeyVault'

Hier volgt een voorbeeld van hoe u een specifieke sleutel tooremove:

AZ keyvault sleutel verwijderen--kluisnaam ContosoKeyVault--de naam 'ContosoFirstKey'

Hier volgt een voorbeeld van hoe u een specifiek geheim tooremove:

AZ keyvault geheim verwijderen--kluisnaam ContosoKeyVault--de naam 'SQLPassword'


## <a name="next-steps"></a>Volgende stappen
Zie voor een volledig overzicht van Azure CLI voor sleutelkluis-opdrachten, [Sleutelkluis CLI-verwijzing](/cli/azure/keyvault)

Zie voor het programmeren van verwijzingen [Hallo ontwikkelaarshandleiding Azure Key Vault](key-vault-developers-guide.md).
