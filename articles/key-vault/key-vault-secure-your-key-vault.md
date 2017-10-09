---
title: aaaSecure uw sleutel vault | Microsoft Docs
description: Toegangsmachtigingen voor Key Vault voor het beheer van kluizen, sleutels en geheimen beheren. Verificatie en autorisatie model voor sleutelkluis en hoe toosecure uw sleutel-kluis
services: key-vault
documentationcenter: 
author: amitbapat
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: e5b4e083-4a39-4410-8e3a-2832ad6db405
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 01/07/2017
ms.author: ambapat
ms.openlocfilehash: 84f5fc18142a1ad89babbd11f4f65eca105afc32
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-your-key-vault"></a>Uw Key Vault beveiligen
Azure Key Vault is een cloudservice die versleutelingssleutels en geheimen (zoals certificaten, verbindingsreeksen en wachtwoorden) voor uw cloudtoepassingen beveiligt. Aangezien deze gegevens vertrouwelijk en kritieke zakelijke is, gewenste toosecure toegang tooyour sleutelkluizen zodat alleen gemachtigde toepassingen en gebruikers hebben toegang tot de sleutelkluis. In dit artikel biedt een overzicht van de sleutelkluis toegangsmodel, verificatie en autorisatie uitgelegd en wordt beschreven hoe toosecure toegang tookey vault voor uw cloudtoepassingen met een voorbeeld.

## <a name="overview"></a>Overzicht
Toegang tooa sleutelkluis wordt geregeld via twee afzonderlijke interfaces: management vlak en het vlak van gegevens. Voor beide vlakken is juiste verificatie en autorisatie vereist voordat een aanroeper (een gebruiker of een toepassing) toegang tookey kluis kunt ophalen. Verificatie stelt Hallo identiteit van de aanroepfunctie hello, terwijl autorisatie bepaalt welke bewerkingen Hallo aanroeper tooperform is toegestaan.

Voor verificatie gebruiken zowel de beheerlaag als de gegevenslaag Azure Active Directory. Voor autorisatie gebruikt het beheervlak op rollen gebaseerd toegangsbeheer (RBAC), terwijl de gegevenslaag het toegangsbeleid van Key Vault gebruikt.

Hier volgt een kort overzicht van Hallo onderwerpen komen aan bod:

[Verificatie met behulp van Azure Active Directory](#authentication-using-azure-active-directory) -deze sectie wordt uitgelegd hoe een aanroeper wordt geverifieerd met Azure Active Directory tooaccess een sleutelkluis via management vlak en vlak van gegevens. 

[Beheerlaag en gegevenslaag](#management-plane-and-data-plane): de beheerlaag en de gegevenslaag zijn twee toegangslagen die worden gebruikt voor toegang tot uw Key Vault. Elke toegangslaag ondersteunt specifieke bewerkingen. Deze sectie beschrijft Hallo toegang eindpunten, bewerkingen ondersteund en toegang tot de control-methode die door elke vlak gebruikt. 

[Toegangsbeheer voor Management vlak](#management-plane-access-control) - In deze sectie zullen we toegang toe te staan toomanagement vlak bewerkingen met behulp van toegangsbeheer op basis van rollen.

[Toegangsbeheer voor gegevens vlak](#data-plane-access-control) -in deze sectie wordt beschreven hoe gegevens van toouse sleutelkluis access policy toocontrol vlak toegang.

[Voorbeeld](#example) -in dit voorbeeld wordt beschreven hoe toosetup toegangsbeheer voor uw sleutelkluis tooallow drie verschillende teams (beveiligingsteam ontwikkelaars/operators en auditors) tooperform specifieke taken toodevelop, beheren en controleren van een toepassing in Azure .

## <a name="authentication-using-azure-active-directory"></a>Verificatie met Azure Active Directory
Wanneer u een sleutelkluis in een Azure-abonnement maakt, is het automatisch gekoppeld aan Azure Active Directory-tenant Hallo-abonnement. Alle aanroepfuncties (gebruikers en toepassingen) moeten worden geregistreerd in deze tenant tooaccess deze sleutelkluis. Een toepassing of een gebruiker moet worden geverifieerd bij Azure Active Directory tooaccess sleutelkluis. Dit geldt tooboth management vlak en gegevens vlak toegang. In beide gevallen kan een toepassing op twee manieren toegang krijgen tot de Key Vault:

* **Toegang voor gebruikers en toepassingen**: meestal is dit voor toepassingen die de Key Vault gebruiken namens een aangemelde gebruiker. Azure PowerShell en Azure Portal zijn voorbeelden van dit type toegang. Er zijn twee manieren toogrant toegang toousers: eenrichtingssessie is toogrant toegang toousers dus sleutelkluis is toegankelijk vanuit elke toepassing en Hallo andere manier is een gebruiker toegang tookey kluis toogrant alleen wanneer ze een bepaalde toepassing (waarnaar wordt verwezen tooas samengestelde identiteit) gebruiken. 
* **App-lezentoegang** : voor toepassingen of daemon services uitvoert, enz. Hallo toepassingsidentiteit is verleend achtergrondtaken toegang toohello tot sleutel kluis.

In beide soorten toepassingen Hallo-aanvraag wordt geverifieerd met Azure Active Directory met behulp van een Hallo [ondersteunde verificatiemethoden](../active-directory/active-directory-authentication-scenarios.md) en krijgt een token. Verificatiemethode die wordt gebruikt, is afhankelijk van het toepassingstype Hallo. Hallo-toepassing wordt vervolgens gebruikt dit token en REST-API-aanvraag tookey kluis verzendt. In geval van een management vlak toegang Hallo worden aanvragen gerouteerd via Azure Resource Manager-eindpunt. Bij het openen van gegevens vlak Hallo toepassingen wordt gesproken rechtstreeks tooa sleutelkluis-eindpunt. Meer informatie Zie op Hallo [hele authenticatiestroom](../active-directory/active-directory-protocols-oauth-code.md). 

Hallo resourcenaam waarvoor toepassing hello een token vraagt verschilt, afhankelijk van of toepassing hello management vlak of vlak van gegevens opent. Hallo resourcenaam is daarom op management vlak of gegevens vlak de eindpunten in de tabel Hallo verderop, afhankelijk van hello Azure-omgeving beschreven.

Een enkel mechanisme voor verificatie tooboth heeft beheer- en vlak een eigen voordelen:

* Organisaties kunnen toegang tooall sleutelkluizen in hun organisatie centraal beheren
* Als een gebruiker verlaat, verliezen ze onmiddellijk toegang tooall sleutelkluizen in Hallo organisatie
* Organisaties kunnen aanpassen verificatie via Hallo-opties in Azure Active Directory (bijvoorbeeld, waardoor multi-factor authentication voor extra beveiliging)

## <a name="management-plane-and-data-plane"></a>De beheer- en gegevenslaag
Azure Key Vault is een Azure-service die beschikbaar is via het Azure Resource Manager-implementatiemodel. Als u een Key Vault hebt gemaakt, krijgt u een virtuele container waarin u andere objecten (zoals sleutels, geheimen en certificaten) kunt maken. Vervolgens opent u de sleutelkluis met vlak en gegevens vlak tooperform specifieke beheerbewerkingen. Vlak beheerinterface is gebruikte toomanage uw sleutel sleutelkluis zelf, zoals het maken, verwijderen, het bijwerken van de kenmerken en het instellen van toegangsbeleid voor gegevens vlak. Gegevens vlak-interface is gebruikte tooadd, verwijderen, wijzigen en gebruik Hallo-sleutels, geheimen en certificaten die zijn opgeslagen in de sleutelkluis.

Hallo vlak en gegevens vlak beheerinterfaces toegankelijk zijn via verschillende eindpunten (Zie tabel). tweede kolom in tabel Hallo Hallo beschrijft Hallo DNS-namen voor deze eindpunten in verschillende Azure-omgevingen. de derde kolom Hallo beschrijft Hallo kunt u bewerkingen vanuit elke vlak toegang uitvoeren. Elke toegangslaag heeft ook een eigen mechanisme voor toegangsbeheer. Het toegangsbeheer voor de beheerlaag wordt ingesteld met behulp van toegangsbeheer op basis van rollen (RBAC) in Azure Resource Manager. Het toegangsbeheer voor de gegevenslaag wordt ingesteld met toegangsbeleid van Key Vault.

| Toegangslaag | Eindpunten voor toegang | Bewerkingen | Mechanisme voor toegangsbeheer |
| --- | --- | --- | --- |
| Beheerlaag |**Wereldwijd:**<br> management.azure.com:443<br><br> **Azure China:**<br> management.chinacloudapi.cn:443<br><br> **Azure van de Amerikaanse overheid:**<br> management.usgovcloudapi.net:443<br><br> **Azure Duitsland:**<br> management.microsoftazure.de:443 |Key Vault maken/lezen/bijwerken/verwijderen <br> Toegangsbeleid voor Key Vault instellen<br>Tags instellen voor Key Vault |Toegangsbeheer op basis van rollen (RBAC) in Azure Resource Manager |
| Gegevenslaag |**Wereldwijd:**<br> &lt;kluisnaam&gt;.vault.azure.net:443<br><br> **Azure China:**<br> &lt;kluisnaam&gt;.vault.azure.cn:443<br><br> **Azure van de Amerikaanse overheid:**<br> &lt;kluisnaam&gt;.vault.usgovcloudapi.net:443<br><br> **Azure Duitsland:**<br> &lt;kluisnaam&gt;.vault.microsoftazure.de:443 |Voor sleutels: Ontsleutelen, Versleutelen, Sleutel uitpakken, Sleutel inpakken, Controleren, Ondertekenen, Ophalen, Sorteren, Bijwerken, Maken, Importeren, Verwijderen, Back-up maken, Herstellen<br><br> Voor geheimen: Ophalen, Sorteren, Instellen, Verwijderen |Toegangsbeleid van Key Vault |

Hallo management vlak en gegevens vlak toegangsbeheer werken onafhankelijk. Bijvoorbeeld, als u een toepassing toouse toegangstoetsen in een sleutelkluis toogrant wilt, hoeft u alleen toogrant vlak machtigingen voor gegevenstoegang met behulp van het toegangsbeleid voor sleutelkluizen en geen vlak management toegang nodig is voor deze toepassing. En als u daarentegen als u wilt dat een gebruiker toobe kunnen tooread vault eigenschappen en labels, maar hebben geen toegang tot tookeys, geheimen of certificaten, kunt u deze gebruiker verlenen, 'read-toegang met RBAC en geen toegang tot toodata vlak is vereist.

## <a name="management-plane-access-control"></a>Toegangsbeheer voor de beheerlaag
Hallo management vlak bestaat uit de bewerkingen die invloed hebben op Hallo sleutelkluis zelf. U kunt bijvoorbeeld een Key Vault maken of verwijderen. U kunt een lijst met Vaults krijgen in een abonnement. U kunt de sleutelkluis-eigenschappen (zoals SKU, tags) ophalen en instellen sleutelkluis toegangsbeleid waarmee Hallo-gebruikers en toepassingen die toegang hebben tot sleutels en geheimen in de sleutelkluis Hallo. Het toegangsbeheer voor de beheerlaag gebruikt RBAC. Overzicht Hallo volledige van sleutelkluis-bewerkingen die kunnen worden uitgevoerd via management vlak in Hallo-tabel in de voorgaande sectie. 

### <a name="role-based-access-control-rbac"></a>Toegangsbeheer op basis van rollen (RBAC)
Elk Azure-abonnement heeft een Azure Active Directory. Toegang tot toomanage bronnen in hello Azure-abonnement met Azure Resource Manager-implementatiemodel Hallo kunnen verleend aan gebruikers, groepen en toepassingen van deze map. Dit type van toegangsbeheer is waarnaar wordt verwezen tooas op rollen gebaseerde toegangsbeheer (RBAC). toomanage dit openen, kunt u Hallo [Azure-portal](https://portal.azure.com/), Hallo [Azure CLI-hulpprogramma's](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), of Hallo [Azure Resource Manager REST-API's](https://msdn.microsoft.com/library/azure/dn906885.aspx).

Met hello Azure Resource Manager-model maakt u de sleutelkluis in een resource group en beheer toegang toohello management vlak van deze sleutelkluis met behulp van Azure Active Directory. U kunt bijvoorbeeld gebruikers of een groep mogelijkheid toomanage sleutelkluizen in een specifieke resourcegroep verlenen.

U kunt toegang toousers, groepen en toepassingen bij een bepaalde scope verlenen door de juiste RBAC-rollen toewijzen. Bijvoorbeeld: toogrant toegang krijgen tot tooa gebruiker toomanage sleutelkluizen zou u een vooraf gedefinieerde rol 'sleutelkluis Inzender' toothis gebruiker op een bepaalde scope toewijzen. Hallo-bereik zou in dit geval zijn een abonnement, resourcegroep of alleen voor een specifieke sleutelkluis. Een rol die is toegewezen op abonnementsniveau geldt tooall resourcegroepen en resources binnen dat abonnement. Een rol heeft op het niveau van de resourcegroep is van toepassing tooall resources in die resourcegroep. Een rol die is toegewezen voor een specifieke bron toothat resource is alleen van toepassing. Er zijn verschillende vooraf gedefinieerde functies (Zie [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md)), en als Hallo vooraf rollen gedefinieerde passen niet uw behoeften kunt u ook uw eigen rollen definiëren.

> [!IMPORTANT]
> Houd er rekening mee dat als een gebruiker Inzender machtigingen (RBAC) tooa sleutelkluis management vlak heeft, ze zichzelf toegang toodata vlak, verlenen kan door in te stellen van de sleutelkluis-beleid, die toegang toodata vlak bepaalt. Daarom wordt aanbevolen tootightly bepalen wie Inzender toegang tooyour sleutelkluizen tooensure alleen daartoe gemachtigde personen kunnen toegang tot en beheer uw sleutelkluizen, sleutels, geheimen en certificaten heeft.
> 
> 

## <a name="data-plane-access-control"></a>Toegangsbeheer voor de gegevenslaag
Hallo sleutelkluis gegevens vlak bestaat uit de bewerkingen die invloed hebben op Hallo-objecten in een sleutelkluis, zoals sleutels, geheimen en certificaten.  Dit zijn onder andere sleutelbewerkingen, zoals sleutels maken, importeren, bijwerken, sorteren, herstellen en er back-ups van maken, cryptografische bewerkingen, zoals ondertekenen, controleren, versleutelen, ontsleutelen, inpakken en uitpakken, en tags en andere kenmerken voor sleutels instellen. Voor geheimen gaat het om bewerkingen zoals ophalen, instellen, sorteren en verwijderen.

U verleent toegang tot de gegevenslaag door toegangsbeleid voor een Key Vault in te stellen. Een gebruiker, groep of een toepassing moet bijdragerrechten (RBAC) voor management vlak voor een sleutelkluis toobe kunnen tooset toegangsbeleid voor die sleutelkluis hebben. Een gebruiker, groep of toepassing kan toegang tooperform specifieke bewerkingen voor sleutels of geheimen in een sleutelkluis te worden verleend. Ondersteuning voor sleutelkluis uit too16 toegang beleid items voor een sleutelkluis. Een Azure Active Directory-beveiligingsgroep maken en toevoegen van gebruikers toothat groep toogrant gegevens vlak toegang tooseveral gebruikers tooa sleutelkluis.

### <a name="key-vault-access-policies"></a>Toegangsbeleid van Key Vault
Het toegangsbeleid voor sleutelkluizen verlenen afzonderlijk machtigingen tookeys, geheimen en certificaten. U kunt bijvoorbeeld een gebruiker toegang tooonly sleutels, maar er zijn geen machtigingen voor geheimen geven. Machtigingen tooaccess sleutels of geheimen of certificaten zijn echter op Hallo kluis niveau. Met andere woorden: het toegangsbeleid voor Key Vault ondersteunt geen machtigingen op objectniveau. U kunt [Azure-portal](https://portal.azure.com/), Hallo [Azure CLI-hulpprogramma's](../cli-install-nodejs.md), [PowerShell](/powershell/azureps-cmdlets-docs), of Hallo [sleutelkluis REST-API's](https://msdn.microsoft.com/library/azure/mt620024.aspx) tooset-beleid voor een sleutelkluis.

> [!IMPORTANT]
> Houd er rekening mee dat het toegangsbeleid voor sleutelkluizen van toepassing op Hallo kluis niveau. Bijvoorbeeld als een gebruiker is verleend machtiging toocreate en delete-sleutels, ze kan deze bewerkingen uitvoeren op alle sleutels in die sleutelkluis.
> 
> 

## <a name="example"></a>Voorbeeld
Stel dat u een toepassing ontwikkelt die gebruikmaakt van een certificaat voor SSL, Azure Storage voor het opslaan van gegevens, en een RSA 2048 bits-sleutel voor tekenbewerkingen. Stel dat deze toepassing wordt uitgevoerd in een VM (of een schaalset voor VM’s). U kunt een sleutelkluis toostore die alle Hallo toepassing geheimen en gebruik sleutelkluis toostore Hallo bootstrap-certificaat dat wordt gebruikt door Hallo toepassing tooauthenticate met Azure Active Directory.

Dus volgt hier een samenvatting weer van alle Hallo sleutels en geheimen toobe opgeslagen in een sleutelkluis.

* **SSL-certificaat**: wordt gebruikt voor SSL
* **Opslagsleutel** -account voor toegang tot tooStorage tooget gebruikt
* **2048-bits RSA-sleutel**: wordt gebruikt voor tekenbewerkingen
* **Bootstrap-certificaat** -tooauthenticate tooAzure Active Directory, tooget tookey kluis toofetch Hallo opslag toegangssleutel en gebruik Hallo RSA-sleutel gebruikt voor het ondertekenen.

Nu gaan we voldoen aan de Hallo mensen die beheren, implementeren en controleren van deze toepassing. In dit voorbeeld gebruiken we drie rollen.

* **Beveiligingsteam** : dit zijn meestal IT-personeel Hallo 'kantoor Hallo CSO (Chief Security Officer)', of gelijkwaardig, is verantwoordelijk voor het Hallo u juiste bewaren geheimen zoals SSL-certificaten, die wordt gebruikt voor het ondertekenen van tekenreeksen voor databaseverbindingen voor RSA-sleutels databases, toegangscodes voor opslag.
* **Ontwikkelaars/operators** -dit zijn Hallo mensen die deze toepassing ontwikkelen en vervolgens te implementeren in Azure. Normaal gesproken ze maken geen deel uit van het beveiligingsteam hello, en daarom moeten ze geen toegang tooany gevoelige gegevens, zoals SSL-certificaten, RSA-sleutels hebben maar Hallo toepassing die ze implementeren toothose toegang moet hebben.
* **Auditors** -dit is meestal een andere set personen, geïsoleerd van Hallo ontwikkelaars en algemene IT-personeel. Hun verantwoordelijkheid is tooreview onjuist wordt gebruikt en het onderhoud van certificaten, sleutels, enz. en ervoor te zorgen dat aan data security standards. 

Er is een meer rol die buiten Hallo bereik van deze toepassing, maar de relevante hier toobe vermeld, en dat is Hallo-abonnement (of resourcegroep) beheerder. Abonnementsbeheerder stelt u initiële toegangsmachtigingen voor Hallo beveiligingsteam. Hier nemen we aan dat abonnement Hallo beheerder toegang toohello team tooa resource beveiligingsgroep waarin alle benodigde resources voor deze toepassing wonen Hallo heeft verleend.

Nu gaan we kijken welke acties elke rol in de context van deze toepassing hello uitvoert.

* **Beveiligingsteam**
  * Key Vaults maken
  * Logboekregistratie van Key Vault inschakelen
  * Sleutels/geheimen toevoegen
  * Back-ups van sleutels maken voor herstel na noodgevallen
  * Beleid toogrant machtigingen toousers en toepassingen tooperform specifieke bewerkingen voor sleutelkluis toegang instellen
  * Sleutels/geheimen periodiek terugdraaien
* **Ontwikkelaars/operators**
  * Verwijzingen toobootstrap en SSL-certificaten klant (vingerafdrukken) opslagsleutel (geheim URI) en de handtekeningsleutel (URI van Key) van het beveiligingsteam ophalen
  * Toepassingen die programmatisch sleutels en geheimen gebruiken, ontwikkelen en implementeren
* **Auditors**
  * Gebruik Logboeken tooconfirm correct sleutel/geheim gebruik en naleving aan data security standards controleren

Nu gaan we kijken welke toegang machtigingen tookey kluis nodig zijn voor elke rol (en de toepassing hello) tooperform hen toegewezen taken. 

| Gebruikersrol | Machtigingen voor de beheerlaag | Machtigingen voor de gegevenslaag |
| --- | --- | --- |
| Beveiligingsteam |Inzender voor Key Vault |Sleutels: back-ups maken, verwijderen, ophalen, importeren, sorteren, herstellen <br> Geheimen: alle |
| Ontwikkelaars/Operators |sleutelkluis machtiging implementeren zodat Hallo VMs ze implementeren kunnen geheimen ophalen van de sleutelkluis Hallo |Geen |
| Auditors |Geen |Sleutels: weergeven<br>Geheimen: weergeven |
| Toepassing |Geen |Sleutels: ondertekenen<br>Geheimen: ophalen |

> [!NOTE]
> Auditors moeten de machtiging voor sleutels en geheimen lijst zodat u ze kunnen inspecteren kenmerken voor sleutels en geheimen die niet worden gegenereerd in Logboeken hello, zoals tags, activering en de vervaldatum.
> 
> 

Naast de machtiging tookey kluis, alle drie functies ook moeten toegang tot tooother bronnen. Bijvoorbeeld: toobe kunnen toodeploy VMs (of Web-Apps enz.) Ontwikkelaars/Operators moet ook 'Inzender' toegang toothose resourcetypen. Auditors moeten leestoegang toohello storage-account waarin Hallo sleutelkluis-logboeken worden opgeslagen.

Aangezien access tooyour sleutelkluis is de beveiliging van dit artikel gericht hello, we alleen illustreren Hallo relevante delen die deel uitmaakt van toothis onderwerp en details met betrekking tot implementatie van certificaten, enzovoort programmatisch toegang van sleutels en geheimen overslaan. Deze informatie wordt elders al behandeld. Implementatie van certificaten die zijn opgeslagen in de sleutelkluis tooVMs vindt u in een [blogbericht](https://blogs.technet.microsoft.com/kv/2016/09/14/updated-deploy-certificates-to-vms-from-customer-managed-key-vault/), en er [voorbeeldcode](https://www.microsoft.com/download/details.aspx?id=45343) beschikbaar die laat zien hoe toouse bootstrap tooauthenticate tooAzure AD tooget certificaat toegang tookey kluis.

De meeste Hallo toegangsmachtigingen kunnen worden verleend via Azure portal, maar toogrant gedetailleerde machtigingen die u wellicht toouse Azure PowerShell (of Azure CLI) tooachieve Hallo gewenst resultaat. 

Hallo na PowerShell codefragmenten wordt ervan uitgegaan dat:

* Hello Azure Active Directory-beheerder heeft beveiligingsgroepen voor Hallo drie rollen, namelijk Contoso beveiligingsteam, Contoso App Devops, Contoso App Auditors gemaakt. Hallo beheerder heeft ook toegevoegd aan gebruikers toohello groepen die ze behoren.
* **ContosoAppRG** Hallo resourcegroep is waarin alle Hallo bronnen zich bevinden. **contosologstorage** waarin Hallo logboeken worden opgeslagen. 
* Sleutelkluis **ContosoKeyVault** en storage-account gebruikt voor sleutelkluis-logboeken **contosologstorage** Hallo moet dezelfde Azure-locatie

Eerste Hallo abonnementsbeheerder toegewezen 'sleutel kluis Inzender' en ' beheerder voor gebruikerstoegang ' rollen toohello beveiligingsteam. Hiermee kan Hallo-team toomanage toegang tooother beveiligingsbronnen en sleutelkluizen in de resourcegroep Hallo ContosoAppRG beheren.

```
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "key vault Contributor" -ResourceGroupName ContosoAppRG
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -RoleDefinitionName "User Access Administrator" -ResourceGroupName ContosoAppRG
```

Hallo volgende script ziet u hoe Hallo beveiligingsteam kunt een sleutelkluis maken, instellen van logboekregistratie en stel toegangsmachtigingen voor andere rollen en het Hallo-toepassing. 

```
# Create key vault and enable logging
$sa = Get-AzureRmStorageAccount -ResourceGroup ContosoAppRG -Name contosologstorage
$kv = New-AzureRmKeyVault -VaultName ContosoKeyVault -ResourceGroup ContosoAppRG -SKU premium -Location 'westus' -EnabledForDeployment
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

# Data plane permissions for Security team
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso Security Team')[0].Id -PermissionsToKeys backup,create,delete,get,import,list,restore -PermissionsToSecrets all

# Management plane permissions for Dev/ops
# Create a new role from an existing role
$devopsrole = Get-AzureRmRoleDefinition -Name "Virtual Machine Contributor"
$devopsrole.Id = $null
$devopsrole.Name = "Contoso App Devops"
$devopsrole.Description = "Can deploy VMs that need secrets from key vault"
$devopsrole.AssignableScopes = @("/subscriptions/<SUBSCRIPTION-GUID>")

# Add permission for dev/ops so they can deploy VMs that have secrets deployed from key vaults
$devopsrole.Actions.Add("Microsoft.KeyVault/vaults/deploy/action")
New-AzureRmRoleDefinition -Role $devopsrole

# Assign this newly defined role tooDev ops security group
New-AzureRmRoleAssignment -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Devops')[0].Id -RoleDefinitionName "Contoso App Devops" -ResourceGroupName ContosoAppRG

# Data plane permissions for Auditors
Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoKeyVault -ObjectId (Get-AzureRmADGroup -SearchString 'Contoso App Auditors')[0].Id -PermissionsToKeys list -PermissionsToSecrets list
```

de aangepaste rol Hallo gedefinieerd, wordt alleen toegewezen toohello abonnement waar Hallo ContosoAppRG resourcegroep wordt gemaakt. Als hello dezelfde aangepaste rollen wordt gebruikt voor andere projecten in andere abonnementen, kan de scope meer abonnementen toegevoegd hebben.

Hallo aangepaste roltoewijzing voor ontwikkelaars Hallo/operators voor Hallo "implementeren/action" machtiging is binnen het bereik toohello resourcegroep. Op deze manier alleen Hallo VMs gemaakt in resourcegroep Hallo 'ContosoAppRG' hello geheimen (SSL-certificaat verstuurd en bootstrap cert) krijgen. Alle virtuele machines die een lid van de dev/ops team in de andere resourcegroep maakt worden niet kunnen tooget deze geheime gegevens zelfs als ze Hallo geheim URI's kent.

In dit voorbeeld ziet u een eenvoudig scenario. Echte leven scenario's mogelijk ingewikkelder en u moet wellicht tooadjust machtigingen tooyour sleutelkluis op basis van uw behoeften. Bijvoorbeeld: in ons voorbeeld gaan we ervan uit dat beveiligingsteam geven Hallo-sleutel en geheime verwijzingen (URI's en vingerafdrukken) die ontwikkelaars/operators team nodig tooreference in hun toepassingen. Daarom hoeven niet ontwikkelaars toogrant/operators vlak toegang tot gegevens. Houd er ook rekening mee dat dit voorbeeld is gericht op het beveiligen van uw Key Vault. Vergelijkbare moet worden overwogen toosecure [uw virtuele machines](https://azure.microsoft.com/services/virtual-machines/security/), [opslagaccounts](../storage/common/storage-security-guide.md) en andere Azure-resources te.

> [!NOTE]
> Opmerking: Dit voorbeeld toont hoe toegang tot de Key Vault wordt vergrendeld tijdens de productie. Hallo ontwikkelaars moeten hebben hun eigen abonnement of resourcegroup waarvoor zij hebben volledige machtigingen toomanage hun kluizen, VM's en storage-account waarin ze Hallo toepassing ontwikkelt.
> 
> 

## <a name="resources"></a>Resources
* [Toegangsbeheer op basis van rollen in Azure Active Directory](../active-directory/role-based-access-control-configure.md)
  
  Dit artikel wordt uitgelegd Hallo toegangsbeheer op basis van een functie van Azure Active Directory en hoe het werkt.
* [RBAC: ingebouwde rollen](../active-directory/role-based-access-built-in-roles.md)
  
  Deze details van alle Hallo ingebouwde rollen die beschikbaar zijn in RBAC.
* [Resource Manager-implementatie en klassieke implementatie begrijpen](../azure-resource-manager/resource-manager-deployment-model.md)
  
  In dit artikel wordt uitgelegd Hallo Resource Manager-implementatie en klassieke implementatiemodel en wordt uitgelegd Hallo voordelen van het gebruik van Hallo Resource Manager en resource-groepen
* [Toegangsbeheer op basis van rollen beheren met Azure PowerShell](../active-directory/role-based-access-control-manage-access-powershell.md)
  
  Dit artikel wordt uitgelegd hoe toomanage rollen gebaseerd toegangsbeheer met Azure PowerShell
* [Toegangsbeheer op basis van rollen met Hallo REST-API beheren](../active-directory/role-based-access-control-manage-access-rest.md)
  
  Dit artikel laat zien hoe toouse Hallo REST-API toomanage RBAC.
* [Toegangsbeheer op basis van rollen voor Microsoft Azure vanuit Ignite](https://channel9.msdn.com/events/Ignite/2015/BRK2707)
  
  Dit is een koppeling tooa video op Channel 9 Hallo 2015 MS Ignite conferentie. In deze sessie, hebben ze over toegang tot beheer- en rapportagefuncties in Azure en bekijk de aanbevolen procedures om de toegang beveiligen tooAzure abonnementen met Azure Active Directory.
* [Toegang tooweb toepassingen met behulp van OAuth 2.0 en Azure Active Directory autoriseren](../active-directory/active-directory-protocols-oauth-code.md)
  
  Dit artikel beschrijft de volledige OAuth 2.0-stroom voor verificatie met Azure Active Directory.
* [Key Vault-beheer met REST-API’s](https://msdn.microsoft.com/library/azure/mt620024.aspx)
  
  Dit document is Hallo-verwijzing voor Hallo REST-API's toomanage uw sleutel vault programmatisch, inclusief het instellen van toegangsbeleid voor sleutelkluis.
* [REST-API’s van Key Vault](https://msdn.microsoft.com/library/azure/dn903609.aspx)
  
  Koppeling tookey kluis REST-API-naslagdocumentatie.
* [Toegangsbeheer voor sleutels](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_KeyAccessControl)
  
  TooSecret access control-naslagdocumentatie koppelen.
* [Toegangsbeheer voor geheimen](https://msdn.microsoft.com/library/azure/dn903623.aspx#BKMK_SecretAccessControl)
  
  TooKey access control-naslagdocumentatie koppelen.
* Toegangsbeleid voor Key Vault [instellen](https://msdn.microsoft.com/library/mt603625.aspx) en [verwijderen](https://msdn.microsoft.com/library/mt619427.aspx) met behulp van PowerShell
  
  Koppelingen tooreference documentatie voor PowerShell-cmdlets toomanage sleutelkluis-beleid.

## <a name="next-steps"></a>Volgende stappen
Zie [Aan de slag met Azure Key Vault](key-vault-get-started.md) voor een inleidende zelfstudie voor beheerders.

Zie [Logboekregistratie van Azure Key Vault](key-vault-logging.md) voor meer informatie over de gebruiksregistratie voor Key Vault.

Zie [Over sleutels en geheimen](https://msdn.microsoft.com/library/azure/dn903623.aspx) voor meer informatie over het gebruik van sleutels en geheimen met Azure Key Vault.

Als u vragen over sleutelkluis hebt, gaat u naar Hallo [Azure sleutelkluis Forums](https://social.msdn.microsoft.com/forums/azure/home?forum=AzureKeyVault)

