---
title: aaaManage werkruimten in de Azure-logboekanalyse en Hallo OMS-portal | Microsoft Docs
description: U kunt de werkruimten in de Azure-logboekanalyse en Hallo OMS-portal met behulp van verschillende beheertaken op gebruikers, accounts, -werkruimten en Azure-accounts beheren.
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: d0e5162d-584b-428c-8e8b-4dcaa746e783
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/06/2017
ms.author: magoedte
ms.openlocfilehash: 570e6c1f13ad28f120ecd65052d00c4ca986ac98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-workspaces"></a>Werkruimten beheren

toomanage toegang tooLog Analytics, dat u gerelateerde tooworkspaces van verschillende beheertaken uitvoeren. Dit artikel vindt aanbevolen toomanage-werkruimten adviezen en procedures. Een werkruimte is in wezen een container waarin gegevens van het account en eenvoudige configuratie-informatie voor Hallo-account. U of andere leden van uw organisatie mogelijk meerdere werkruimten toomanage verschillende sets van gegevens die worden verzameld uit alle of delen van uw IT-infrastructuur gebruiken.

een werkruimte toocreate, moet u:

1. U dient een Azure-abonnement te hebben.
2. U dient een naam voor de werkruimte te kiezen.
3. Hallo-werkruimte koppelen aan uw abonnement.
4. U dient een geografische locatie te kiezen.

## <a name="determine-hello-number-of-workspaces-you-need"></a>Hallo aantal werkruimten, u moet bepalen
Een werkruimte is een Azure-resource en is een container waarin gegevens wordt verzameld, geaggregeerd geanalyseerd en die zijn gepresenteerd in hello Azure-portal.

U kunt meerdere werkruimten per Azure-abonnement hebben en u toomore toegang kan hebben dan een werkruimte. Minimalisatie van het aantal Hallo aantal werkruimten kunt u tooquery en correleren op Hallo van de meeste gegevens, omdat het niet mogelijk tooquery over meerdere werkruimten. Deze sectie wordt beschreven wanneer het kan ook nuttig toocreate meer dan één werkruimte.

Een werkruimte biedt momenteel het volgende:

* Een geografische locatie voor de opslag van gegevens
* Details voor facturering
* Gegevensisolatie
* Bereik voor configuratie

Op basis van kenmerken voorgaande Hallo, kunt u toocreate meerdere werkruimten als:

* U vertegenwoordigt een mondiaal bedrijf en moet de gegevens opslaan in specifieke regio’s ten behoeve van de onafhankelijkheid van de gegevens of om nalevingsredenen.
* U gebruikt Azure en u wilt dat de uitgaande gegevensoverdracht tooavoid kosten doordat een werkruimte dezelfde regio Hallo zoals hello Azure-resources beheert.
* U wilt tooallocate kosten toodifferent afdelingen of bedrijfsgroepen op basis van hun gebruik. Bij het maken van een werkruimte voor elke afdeling of bedrijfsgroep wordt uw Azure factuur- en gebruiksgegevens instructie Hallo kosten voor elke werkruimte afzonderlijk.
* U provider van beheerde services en moet tookeep Hallo log analytics-gegevens voor elke klant die u beheert, geïsoleerd van gegevens van andere klanten.
* Beheren van meerdere klanten en u wilt dat elke klant / afdeling / business groep toosee hun eigen gegevens, maar niet Hallo-gegevens voor anderen.

Wanneer u agents toocollect gegevens gebruikt, kunt u [configureren van elke agent tooreport tooone of meer werkruimten](log-analytics-windows-agents.md).

Als u System Center Operations Manager gebruikt, kan elke beheergroep uit Operations Manager worden verbonden met slechts één werkruimte. U kunt Hallo Microsoft Monitoring Agent installeren op computers die worden beheerd door Operations Manager en Hallo agent rapport tooboth Operations Manager en een andere werkruimte voor logboekanalyse.

### <a name="workspace-information"></a>Werkruimtegegevens

U kunt details weergeven over uw werkruimte in hello Azure-portal. U kunt ook details weergeven in Hallo OMS-portal.

#### <a name="view-workspace-information-in-hello-azure-portal"></a>Werkruimte informatie weergeven in hello Azure-portal

1. Als u dit nog niet hebt gedaan, meld u aan toohello [Azure-portal](https://portal.azure.com) met behulp van uw Azure-abonnement.
2. Op Hallo **Hub** menu, klikt u op **meer services** en typt u in de lijst met resources Hallo **logboekanalyse**. Als u te typen begint, Hallo lijstfilters op basis van uw invoer. Klik op **Log Analytics**.  
    ![Azure-hub](./media/log-analytics-manage-access/hub.png)  
3. Selecteer een werkruimte in Hallo logboekanalyse abonnementen blade.
4. Hallo werkruimte blade geeft details weer over Hallo werkruimte en koppelingen naar aanvullende informatie.  
    ![details van de werkruimte](./media/log-analytics-manage-access/workspace-details.png)  


## <a name="manage-accounts-and-users"></a>Accounts en gebruikers beheren
Elke werkruimte kan meerdere accounts die zijn gekoppeld, en elke account (Microsoft-account of organisatie-account) toegang toomultiple werkruimten kan hebben.

Hallo-Microsoft-account of organisatie-account dat Hallo werkruimte maakt, wordt standaard Hallo beheerder van Hallo-werkruimte.

Er zijn twee modellen van machtigingen waarmee access tooa Log Analytics-werkruimte:

1. Verouderde Log Analytics-gebruikersrollen
2. [Toegang op basis van rollen in Azure](../active-directory/role-based-access-control-configure.md)

Hallo volgende tabel geeft een overzicht van Hallo toegang kan worden ingesteld met behulp van elk model machtiging:

|                          | Log Analytics-portal | Azure Portal | API (inclusief PowerShell) |
|--------------------------|----------------------|--------------|----------------------------|
| Log Analytics-gebruikersrollen | Ja                  | Nee           | Nee                         |
| Toegang op basis van rollen in Azure  | Ja                  | Ja          | Ja                        |

> [!NOTE]
> Log Analytics verplaatst toouse Azure op rollen gebaseerde toegang als Hallo machtigingenmodel vervangen Hallo Log Analytics-gebruikersrollen.
>
>

Hallo verouderde Log Analytics-gebruikersrollen bepaalt alleen toegang tooactivities uitgevoerd in Hallo [logboekanalyseportal](https://mms.microsoft.com).

Hallo na activiteiten ook Azure machtigingen zijn vereist:

| Actie                                                          | Azure-machtigingen nodig | Opmerkingen |
|-----------------------------------------------------------------|--------------------------|-------|
| Beheeroplossingen toevoegen en verwijderen                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/*` <br> `Microsoft.OperationsManagement/*` <br> `Microsoft.Automation/*` <br> `Microsoft.Resources/deployments/*/write` | |
| Hallo prijscategorie wijzigen                                       | `Microsoft.OperationalInsights/workspaces/*/write` | |
| Gegevens weergeven in Hallo *back-up* en *siteherstel* oplossing tegels | Beheerder/medebeheerder | Toegang tot resources geïmplementeerd met het klassieke implementatiemodel Hallo |
| Maken van een werkruimte in hello Azure-portal                        | `Microsoft.Resources/deployments/*` <br> `Microsoft.OperationalInsights/workspaces/*` ||


### <a name="managing-access-toolog-analytics-using-azure-permissions"></a>Het beheren van toegang tot tooLog Analytics met Azure machtigingen
toogrant toegang toohello werkruimte voor logboekanalyse met behulp van Azure machtigingen Hallo stappen in [rol toewijzingen toomanage toegang tooyour Azure-abonnementresources gebruiken](../active-directory/role-based-access-control-configure.md).

Azure heeft twee ingebouwde gebruikersrollen voor Log Analytics:
- Lezer van Log Analytics
- Inzender van Log Analytics

Leden van Hallo *Analytics logboekweergave* rol kunt:
- Alle controlegegevens weergeven en doorzoeken 
- Controle-instellingen, inclusief Hallo configuratie van Azure diagnostics weergeven op alle Azure-resources weergeven.

| Type    | Machtiging | Beschrijving |
| ------- | ---------- | ----------- |
| Actie | `*/read`   | Mogelijkheid tooview alle resources en resourceconfiguratie. Omvat: <br> Status van de VM-extensie <br> Configuratie van Azure Diagnostics voor resources <br> Alle eigenschappen en instellingen van alle resources |
| Actie | `Microsoft.OperationalInsights/workspaces/analytics/query/action` | Mogelijkheid tooperform logboek zoeken v2-query 's |
| Actie | `Microsoft.OperationalInsights/workspaces/search/action` | Mogelijkheid tooperform logboek zoeken v1-query 's |
| Actie | `Microsoft.Support/*` | Mogelijkheid tooopen ondersteuningsaanvragen |
|Geen bewerking | `Microsoft.OperationalInsights/workspaces/sharedKeys/read` | Voorkomt dat het lezen van de werkruimte sleutel vereist toouse Hallo gegevens verzameling API en tooinstall agents |


Leden van Hallo *Log Analytics Inzender* rol kunt:
- Alle controlegegevens lezen 
- Automation-accounts maken en configureren
- Beheeroplossingen toevoegen en verwijderen
- Opslagaccountsleutels lezen 
- Verzameling met logboeken uit Azure Storage configureren
- De controle-instellingen voor Azure-resources bewerken, inclusief
  - Hallo VM-extensie tooVMs toevoegen
  - Azure Diagnostics configureren op alle Azure-resources

> [!NOTE] 
> U kunt Hallo mogelijkheid tooadd een virtuele machine extensie tooa virtuele machine toogain volledige controle over een virtuele machine.

| Machtiging | Beschrijving |
| ---------- | ----------- |
| `*/read`     | Mogelijkheid tooview alle resources en resourceconfiguratie. Omvat: <br> Status van de VM-extensie <br> Configuratie van Azure Diagnostics voor resources <br> Alle eigenschappen en instellingen van alle resources |
| `Microsoft.Automation/automationAccounts/*` | Mogelijkheid toocreate en configureren van Azure Automation-accounts, inclusief het toevoegen en bewerken van runbooks |
| `Microsoft.ClassicCompute/virtualMachines/extensions/*` <br> `Microsoft.Compute/virtualMachines/extensions/*` | Toevoegen, bijwerken en verwijderen van virtuele machine extensies, met inbegrip van Hallo Microsoft Monitoring Agent-extensie en Hallo OMS-Agent voor Linux-extensie |
| `Microsoft.ClassicStorage/storageAccounts/listKeys/action` <br> `Microsoft.Storage/storageAccounts/listKeys/action` | Weergave Hallo opslagaccountsleutel. Vereist tooconfigure logboekanalyse tooread logboeken van Azure storage-accounts |
| `Microsoft.Insights/alertRules/*` | Waarschuwingsregels toevoegen, bijwerken en verwijderen |
| `Microsoft.Insights/diagnosticSettings/*` | Diagnostische instellingen bij Azure-resources toevoegen, bijwerken en verwijderen |
| `Microsoft.OperationalInsights/*` | Configuratie voor Log Analytics-werkruimten toevoegen, bijwerken en verwijderen |
| `Microsoft.OperationsManagement/*` | Beheeroplossingen toevoegen en verwijderen |
| `Microsoft.Resources/deployments/*` | Maak en verwijder implementaties. Vereist voor het toevoegen en verwijderen van oplossingen, werkruimten en Automation-accounts |
| `Microsoft.Resources/subscriptions/resourcegroups/deployments/*` | Maak en verwijder implementaties. Vereist voor het toevoegen en verwijderen van oplossingen, werkruimten en Automation-accounts |

tooadd en verwijder gebruikers tooa gebruikersrol, is het nodig toohave `Microsoft.Authorization/*/Delete` en `Microsoft.Authorization/*/Write` machtiging.

Het gebruik van deze rollen toogive gebruikerstoegang op verschillende bereiken:
- Abonnement - toegang tooall werkruimten in Hallo-abonnement
- Resourcegroep - Access tooall-werkruimte in de resourcegroep Hallo
- Bron - toegang tooonly Hallo opgegeven werkruimte

Gebruik [aangepaste rollen](../active-directory/role-based-access-control-custom-roles.md) toocreate rollen met Hallo specifieke machtigingen die nodig zijn.

### <a name="azure-user-roles-and-log-analytics-portal-user-roles"></a>Gebruikersrollen in Azure en in Log Analytics-portal
Als u op Azure minimaal leesmachtiging voor werkruimte voor logboekanalyse hello, kunt u Hallo Log Analytics-portal openen door te klikken op Hallo **OMS-Portal** wanneer u bekijkt hello Log Analytics-werkruimte van de taak.

Bij het openen van Hallo-logboekanalyseportal overschakelen toousing Hallo verouderde Log Analytics-gebruikersrollen. Als u geen roltoewijzing in Hallo Log Analytics-portal, Hallo service [controles hello Azure machtigingen die u op Hallo werkruimte hebt](https://docs.microsoft.com/rest/api/authorization/permissions#Permissions_ListForResource).
De roltoewijzing in Hallo Log Analytics-portal wordt bepaald met behulp van als volgt:

| Voorwaarden                                                   | Toegewezen Log Analytics-gebruikersrol | Opmerkingen |
|--------------------------------------------------------------|----------------------------------|-------|
| Uw account behoort tooa verouderde Log Analytics-gebruikersrol     | Hallo opgegeven gebruikersrol Log Analytics | |
| Uw account hoort niet tooa verouderde Log Analytics-gebruikersrol <br> Volledige Azure machtigingen toohello werkruimte (`*` machtiging <sup>1</sup>) | Beheerder ||
| Uw account hoort niet tooa verouderde Log Analytics-gebruikersrol <br> Volledige Azure machtigingen toohello werkruimte (`*` machtiging <sup>1</sup>) <br> *geen acties* van `Microsoft.Authorization/*/Delete` en `Microsoft.Authorization/*/Write` | Inzender ||
| Uw account hoort niet tooa verouderde Log Analytics-gebruikersrol <br> Azure-leesmachtiging | Alleen-lezen ||
| Uw account hoort niet tooa verouderde Log Analytics-gebruikersrol <br> Azure-machtigingen zijn niet begrepen | Alleen-lezen ||
| Voor door Cloud Solution Provider (CSP) beheerde abonnementen <br> u aangemeld met bent Hallo-account is in hello Azure Active Directory gekoppeld toohello werkruimte | Beheerder | Doorgaans Hallo klant van een CSP |
| Voor door Cloud Solution Provider (CSP) beheerde abonnementen <br> u aangemeld met bent Hallo-account is niet in hello Azure Active Directory gekoppeld toohello werkruimte | Inzender | Doorgaans Hallo CSP |

<sup>1</sup> te verwijzen[Azure machtigingen](../active-directory/role-based-access-control-custom-roles.md) voor meer informatie over roldefinities. Bij het evalueren van functies, een actie van `*` is niet te worden equivalent`Microsoft.OperationalInsights/workspaces/*`.

Sommige tookeep punten in gedachten over hello Azure-portal:

* Wanneer u zich aanmeldt toohello OMS-portal met behulp van http://mms.microsoft.com, ziet u Hallo **Selecteer een werkruimte** lijst. Deze lijst bevat alleen werkruimten waarin u een Log Analytics-gebruikersrol hebt. toosee hello werkruimten die u hebt toegang tot toowith Azure-abonnementen, moet u een tenant toospecify als onderdeel van het Hallo-URL. Bijvoorbeeld `mms.microsoft.com/?tenant=contoso.com`. Hallo tenant-id is vaak het laatste onderdeel van Hallo e-mailadres dat u toosign in.
* Als u wilt dat toonavigate direct tooa-portal die u hebt toegang tot Azure toousing machtigingen, dan hebt u nodig hebt toospecify Hallo resource als onderdeel van het Hallo-URL. Het is mogelijk tooget deze URL met behulp van PowerShell.

  Bijvoorbeeld `(Get-AzureRmOperationalInsightsWorkspace).PortalUrl`.

  Hallo URL ziet eruit als:`https://eus.mms.microsoft.com/?tenant=contoso.com&resource=%2fsubscriptions%2faaa5159e-dcf6-890a-a702-2d2fee51c102%2fresourcegroups%2fdb-resgroup%2fproviders%2fmicrosoft.operationalinsights%2fworkspaces%2fmydemo12`

### <a name="managing-users-in-hello-oms-portal"></a>Het beheren van gebruikers in Hallo OMS-portal
Beheren van gebruikers en groepen op Hallo **gebruikers beheren** tabblad onder Hallo **Accounts** tabblad in Hallo instellingenpagina.   

![gebruikers beheren](./media/log-analytics-manage-access/setup-workspace-manage-users.png)


#### <a name="add-a-user-tooan-existing-workspace"></a>Een bestaande gebruiker tooan-werkruimte toevoegen
Volgende stappen tooadd een gebruiker of groep tooa werkruimte Hallo gebruiken.

1. Klik in het Hallo-OMS-portal op Hallo **instellingen** tegel.
2. Klik op Hallo **Accounts** tabblad en klik vervolgens op Hallo **gebruikers beheren** tabblad.
3. In Hallo **gebruikers beheren** sectie, kiest u Hallo account type tooadd: **Organisatieaccount**, **Microsoft-Account**, **Microsoft Support**.

   * Als u ervoor kiest de Microsoft-Account, typt u Hallo e-mailadres van Hallo-gebruiker is gekoppeld aan Hallo Microsoft-Account.
   * Als u Organisatieaccount kiest, voer deel van de gebruiker Hallo / van de groep naam of e-mailalias en een lijst met overeenkomende gebruikers en groepen weergegeven in de vervolgkeuzelijst. Selecteer een gebruiker of groep.
   * Gebruik Microsoft Support toogive een Microsoft Support engineer of andere Microsoft werknemer tijdelijk toegang tooyour werkruimte toohelp op te lossen.

     > [!NOTE]
     > Voor de beste prestaties Hallo Hallo aantal beperken van Active Directory-groepen die zijn gekoppeld aan een enkele OMS account toothree: één voor beheerders, één voor de medewerkers en één voor alleen-lezen. Met behulp van meer groepen mogelijk invloed op prestaties Hallo van logboekanalyse.
     >
     >
4. Hallo-type van de gebruiker of groep tooadd kiezen: **beheerder**, **Inzender**, of **ReadOnly gebruiker**.  
5. Klik op **Add**.

   Als u een Microsoft-account toevoegt, wordt een uitnodiging toojoin Hallo werkruimte toohello e-mail die u hebt opgegeven verzonden. Nadat de gebruiker Hallo volgt Hallo-instructies in Hallo uitnodiging toojoin OMS, toegankelijk Hallo gebruiker Hallo werkruimte.
   Als u een organisatie-account toevoegt, Hallo gebruiker toegang tot logboekanalyse onmiddellijk.  

#### <a name="edit-an-existing-user-type"></a>Een bestaand gebruikerstype bewerken
U kunt Hallo Accountrol voor een gebruiker die is gekoppeld aan uw account OMS wijzigen. Hebt u Hallo rol opties te volgen:

* *Beheerder*: kan gebruikers beheren, alle waarschuwingen weergeven en er actie voor ondernemen, en servers toevoegen en verwijderen
* *Bijdrager*: kan alle waarschuwingen weergeven en er actie voor ondernemen, en servers toevoegen en verwijderen
* *Gebruiker met alleen-lezentoegang*: gebruikers die zijn gemarkeerd als alleen-lezen kunnen het volgende niet:

  1. Oplossingen toevoegen/verwijderen. Hallo Oplossingengalerie is verborgen.
  2. Tegels toevoegen/wijzigen/verwijderen in **Mijn dashboard**.
  3. Weergave Hallo **instellingen** pagina's. Hallo-pagina's zijn verborgen.
  4. In de zoekweergave van het Hallo, Power BI-configuratie, opgeslagen zoekacties en waarschuwingen zijn taken verborgen.

#### <a name="tooedit-an-account"></a>tooedit een account
1. Klik in het Hallo-OMS-portal op Hallo **instellingen** tegel.
2. Klik op Hallo **Accounts** tabblad en klik vervolgens op Hallo **gebruikers beheren** tabblad.
3. Selecteer de rol Hallo voor Hallo-gebruiker die u toochange wilt.
4. Klik in het bevestigingsdialoogvenster Hallo op **Ja**.

### <a name="remove-a-user-from-a-workspace"></a>Een gebruiker uit een werkruimte verwijderen
Volgende stappen tooremove een gebruiker uit een werkruimte hello gebruiken. Verwijderen Hallo gebruiker Hallo-werkruimte niet gesloten. In plaats daarvan verwijdert deze Hallo koppeling tussen die gebruiker en het Hallo-werkruimte. Als een gebruiker gekoppeld aan meerdere werkruimten is, wel nog steeds die gebruiker aanmelden tooOMS en hun andere werkruimtes zien.

1. Klik in het Hallo-OMS-portal op Hallo **instellingen** tegel.
2. Klik op Hallo **Accounts** tabblad en klik vervolgens op Hallo **gebruikers beheren** tabblad.
3. Klik op **verwijderen** volgende toohello gebruikersnaam die u tooremove wilt.
4. Klik in het bevestigingsdialoogvenster Hallo op **Ja**.

### <a name="add-a-group-tooan-existing-workspace"></a>Een bestaande groep tooan-werkruimte toevoegen
1. Volg de stappen 1-4 in Hallo voorafgaand aan de sectie 'een bestaande werkruimte van gebruiker tooan tooadd'.
2. Selecteer onder **Gebruiker/groep kiezen** de optie **Groep**.  
   ![een bestaande groep tooan-werkruimte toevoegen](./media/log-analytics-manage-access/add-group.png)
3. Hallo weergegeven naam of e-mailadres invoeren voor de groep Hallo gewenst tooadd.
4. Selecteer Hallo in Hallo lijst resultaten en klik vervolgens op **toevoegen**.

## <a name="link-an-existing-workspace-tooan-azure-subscription"></a>Koppelen van een bestaande werkruimte tooan Azure-abonnement
Alle werkruimten die zijn gemaakt na 26 September 2016 moet gekoppelde tooan Azure-abonnement tijdens het maken. Werkruimten die zijn gemaakt vóór deze datum moet gekoppelde tooa werkruimte wanneer u zich aanmeldt. Wanneer u Hallo-werkruimte van hello Azure-portal maakt, of wanneer u uw werkruimte tooan Azure-abonnement koppelen, wordt uw Azure Active Directory als uw organisatie-account gekoppeld.

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-oms-portal"></a>toolink een werkruimte tooan Azure-abonnement in Hallo OMS-portal

- Wanneer u zich bij Hallo OMS-portal aanmeldt, bent u na vragen aan gebruiker tooselect een Azure-abonnement. Selecteer Hallo-abonnement dat u wilt dat toolink tooyour werkruimte en klik vervolgens op **koppeling**.  
    ![Azure-abonnement koppelen](./media/log-analytics-manage-access/required-link.png)

    > [!IMPORTANT]
    > een werkruimte toolink, uw Azure-account moet toegang toohello werkruimte die u wilt dat toolink al hebben.  Met andere woorden, Hallo account waarmee u tooaccess hello Azure-portal moet **Hallo dezelfde** als Hallo account waarmee u tooaccess Hallo werkruimte. Als dit niet het geval is, Zie [toevoegen van een bestaande werkruimte van gebruiker tooan](#add-a-user-to-an-existing-workspace).

### <a name="toolink-a-workspace-tooan-azure-subscription-in-hello-azure-portal"></a>toolink een werkruimte tooan Azure-abonnement in hello Azure-portal
1. Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).
2. Blader naar **Log Analytics** en selecteer dit.
3. U ziet de lijst met bestaande werkruimten. Klik op **Add**.  
   ![lijst met werkruimten](./media/log-analytics-manage-access/manage-access-link-azure01.png)
4. Klik onder **OMS-werkruimte** op **Of bestaande koppelen**.  
   ![bestaande koppelen](./media/log-analytics-manage-access/manage-access-link-azure02.png)
5. Klik op **Vereiste instellingen configureren**.  
   ![vereiste instellingen configureren](./media/log-analytics-manage-access/manage-access-link-azure03.png)
6. U ziet het Hallo-lijst van werkruimten die niet zijn gekoppeld nog tooyour Azure-account. Selecteer een werkruimte.  
   ![werkruimten selecteren](./media/log-analytics-manage-access/manage-access-link-azure04.png)
7. Indien nodig, kunt u waarden voor de volgende items Hallo wijzigen:
   * Abonnement
   * Resourcegroep
   * Locatie
   * Prijscategorie  
     ![waarden wijzigen](./media/log-analytics-manage-access/manage-access-link-azure05.png)
8. Klik op **OK**. Hallo-werkruimte is nu gekoppelde tooyour Azure-account.

> [!NOTE]
> Als er geen Hallo werkruimte gewenst toolink vervolgens uw Azure-abonnement heeft geen toegang tot toohello werkruimte dat u met de Hallo OMS-portal gemaakt.  account voor toegang tot toothis toogrant van Hallo OMS-portal, Zie [toevoegen van een bestaande werkruimte van gebruiker tooan](#add-a-user-to-an-existing-workspace).
>
>

## <a name="upgrade-a-workspace-tooa-paid-plan"></a>Upgrade van een werkruimte tooa betaald abonnement
Er zijn drie typen werkruimteabonnementen voor OMS: **Gratis**, **Zelfstandig** en **OMS**.  Als u op Hallo *vrije* plannen, wordt er een limiet van 500 MB aan gegevens per dag verzonden tooLog Analytics.  Als u deze hoeveelheid overschrijdt, moet u toochange uw werkruimte tooa betaald abonnement tooavoid niet verzamelen van gegevens boven deze limiet. U kunt op elk gewenst moment uw type abonnement wijzigen.  Zie [Prijsgegevens](https://www.microsoft.com/en-us/cloud-platform/operations-management-suite-pricing) voor meer informatie over de tarieven voor OMS.

### <a name="using-entitlements-from-an-oms-subscription"></a>Rechten van een OMS-abonnement gebruiken
toouse hello rechten die afkomstig zijn van het aanschaffen van een OMS-E1, OMS E2 OMS of OMS-invoegtoepassing voor System Center, kies Hallo *OMS* plan van logboekanalyse OMS.

Wanneer u een OMS-abonnement koopt, Hallo rechten tooyour Enterprise Agreement toegevoegd. Een Azure-abonnement dat wordt gemaakt onder deze overeenkomst kunt Hallo rechten. Alle werkruimten op deze abonnementen gebruiken Hallo OMS rechten.

tooensure dat informatie over het gebruik van een werkruimte toegepaste tooyour rechten van Hallo OMS-abonnement is, moet u:

1. Uw werkruimte in een Azure-abonnement dat deel uitmaakt van Hallo Enterprise-overeenkomst met Hallo OMS-abonnement maken
2. Selecteer Hallo *OMS* Hallo werkruimte plannen

> [!NOTE]
> Als uw werkruimte is gemaakt voordat 26 September 2016 en uw Log Analytics plan prijzen *Premium*, wordt deze werkruimte rechten van Hallo OMS-invoegtoepassing voor System Center. U kunt ook uw rechten door het wijzigen van toohello *OMS* prijscategorie.
>
>

Hallo OMS abonnement rechten zijn niet zichtbaar in hello Azure of OMS-portal. U kunt zien rechten en gebruik in Hallo Enterprise Portal.  

Als u toochange Hallo uw werkruimte is gekoppeld aan Azure-abonnement nodig hebt, kunt u Azure PowerShell Hallo [verplaatsen AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.

### <a name="using-azure-commitment-from-an-enterprise-agreement"></a>Azure Commitment gebruiken via een Enterprise-overeenkomst
Als u niet een OMS-abonnement hebt, betaalt u voor elk onderdeel van OMS afzonderlijk en Hallo gebruik wordt weergegeven op uw Azure-factuur.

Als u Azure maandbedrag op Hallo enterprise-inschrijving toowhich uw Azure-abonnementen worden gekoppeld, informatie over het gebruik van logboekanalyse automatisch wordt afgetrokken van tegen Hallo resterende bedrag doorvoeren.

Als u moet toochange hello Azure-abonnement dat Hallo werkruimte is gekoppeld, kunt u Azure PowerShell Hallo [verplaatsen AzureRmResource](https://msdn.microsoft.com/library/mt652516.aspx) cmdlet.  

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-azure-portal"></a>Wijzigen van een werkruimte tooa betaald prijscategorie hello Azure-portal
1. Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).
2. Blader naar **Log Analytics** en selecteer dit.
3. U ziet de lijst met bestaande werkruimten. Selecteer een werkruimte.  
4. Hallo werkruimte blade onder **algemene**, klikt u op **prijscategorie**.  
5. Selecteer onder **Prijscategorie** een prijscategorie en klik vervolgens op **Selecteren**.  
    ![abonnement selecteren](./media/log-analytics-manage-access/manage-access-change-plan03.png)
6. Wanneer u uw weergave in hello Azure-portal vernieuwt, ziet u **prijscategorie** bijgewerkt voor Hallo laag die u hebt geselecteerd.  
    ![bijgewerkt abonnement](./media/log-analytics-manage-access/manage-access-change-plan04.png)

> [!NOTE]
> Als uw werkruimte gekoppelde tooan Automation-account is, voordat u kunt selecteren Hallo *zelfstandige (Per GB)* prijscategorie moet u alle verwijderen **Automation en Control** oplossingen en Hallo Automation ontkoppelen account. Hallo werkruimte blade onder **algemene**, klikt u op **oplossingen** toosee en delete-oplossingen. toounlink hello Automation-account, klikt u op Hallo-naam van Automation-account op Hallo Hallo **prijscategorie** blade.
>
>

### <a name="change-a-workspace-tooa-paid-pricing-tier-in-hello-oms-portal"></a>Wijzigen van een werkruimte tooa betaald prijscategorie Hallo OMS-portal

toochange Hallo prijscategorie Hallo OMS-portal te gebruiken, moet u een Azure-abonnement hebben.

1. Klik in het Hallo-OMS-portal op Hallo **instellingen** tegel.
2. Klik op Hallo **Accounts** tabblad en klik vervolgens op Hallo **Azure-abonnement & Data-abonnement** tabblad.
3. Klik op de prijscategorie die u wilt dat toouse Hallo.
4. Klik op **Opslaan**.  
   ![abonnement en data-abonnementen](./media/log-analytics-manage-access/subscription-tab.png)

Uw nieuwe data-abonnement wordt in Hallo OMS-portal lint Hallo boven aan de webpagina weergegeven.

![OMS-lint](./media/log-analytics-manage-access/data-plan-changed.png)


## <a name="change-how-long-log-analytics-stores-data"></a>Wijzigen hoelang gegevens worden opgeslagen in Log Analytics

Op Hallo gratis prijscategorie, maakt Log Analytics beschikbaar Hallo laatste zeven dagen aan gegevens.
Log Analytics maakt beschikbaar Hallo afgelopen 30 dagen van gegevens op Hallo standaard prijscategorie.
Log Analytics maakt beschikbaar Hallo afgelopen 365 dagen van gegevens op Hallo Premium prijscategorie.
Log Analytics maakt beschikbaar Hallo afgelopen 31 dagen van gegevens op Hallo zelfstandige en OMS Prijscategorieën standaard.

Wanneer u zelfstandige Hallo en OMS Prijscategorieën, kun je up too2 jaar gegevens (730 dagen). Gegevens langer dan de standaardwaarde Hallo van 31 dagen opgeslagen leidt ertoe dat gegevens bewaren kosten met zich mee. Zie [Overschrijdingskosten](https://azure.microsoft.com/pricing/details/log-analytics/) voor meer informatie.

toochange hello lengte van het bewaren van gegevens:

1. Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).
2. Blader naar **Log Analytics** en selecteer dit.
3. U ziet de lijst met bestaande werkruimten. Selecteer een werkruimte.  
4. Hallo werkruimte blade onder **algemene**, klikt u op **bewaren**.  
5. Hallo schuifregelaar tooincrease of verminder het aantal dagen bewaren Hallo en klik vervolgens op **opslaan**.  
    ![retentie wijzigen](./media/log-analytics-manage-access/manage-access-change-retention01.png)

## <a name="change-an-azure-active-directory-organization-for-a-workspace"></a>Een Azure Active Directory-organisatie wijzigen voor een werkruimte

U kunt de Azure Active Directory-organisatie van een werkruimte wijzigen. Veranderende hello Azure Active Directory-organisatie kunt u tooadd gebruikers en groepen in die map toohello werkruimte.

### <a name="toochange-hello-azure-active-directory-organization-for-a-workspace"></a>toochange hello Azure Active Directory-organisatie voor een werkruimte

1. Klik op de instellingenpagina Hallo in Hallo OMS-portal, **Accounts** en klik vervolgens op Hallo **gebruikers beheren** tabblad.  
2. Hallo informatie bekijken over organisatieaccounts en klik vervolgens op **wijziging organisatie**.  
    ![organisatie wijzigen](./media/log-analytics-manage-access/manage-access-add-adorg01.png)
3. Voer Hallo identiteitsgegevens voor Hallo beheerder van uw Azure Active Directory-domein. Hierna ziet u een bevestiging dat uw werkruimte gekoppelde tooyour Azure Active Directory-domein is.  
    ![bevestiging van gekoppelde werkruimte](./media/log-analytics-manage-access/manage-access-add-adorg02.png)


## <a name="delete-a-log-analytics-workspace"></a>Een Log Analytics-werkruimte verwijderen
Wanneer u een werkruimte voor logboekanalyse verwijdert, worden alle gegevens gerelateerd tooyour werkruimte wordt verwijderd uit Hallo OMS-service binnen 30 dagen.

Als u een beheerder bent en er meerdere gebruikers die zijn gekoppeld aan het Hallo-werkruimte zijn, zijn Hallo koppeling tussen die gebruikers en het Hallo-werkruimte is verbroken. Als gebruikers Hallo gekoppeld aan andere werkruimtes zijn, kunnen ze vervolgens blijven OMS gebruiken met die andere werkruimtes. Als ze niet gekoppeld aan andere werkruimtes zijn vervolgens moeten zij toocreate een werkruimte toouse OMS.

### <a name="toodelete-a-workspace"></a>toodelete een werkruimte
1. Meld u aan bij Hallo [Azure-portal](http://portal.azure.com).
2. Blader naar **Log Analytics** en selecteer dit.
3. U ziet de lijst met bestaande werkruimten. Hallo-werkruimte die u toodelete wilt selecteren.
4. Klik op Hallo werkruimte blade **verwijderen**.  
    ![verwijderen](./media/log-analytics-manage-access/delete-workspace01.png)
5. Klik in het dialoogvenster voor bevestiging Hallo verwijderen werkruimte, op **Ja**.

## <a name="next-steps"></a>Volgende stappen
* Zie [verbinding maken met Windows-computers tooLog Analytics](log-analytics-windows-agents.md) tooadd agents en gegevens te verzamelen.
* [Log Analytics-oplossingen van Hallo oplossingen galerie toevoegen](log-analytics-add-solutions.md) tooadd functionaliteit en verzamelen gegevens.
* [Proxy- en firewall-instellingen configureren in logboekanalyse](log-analytics-proxy-firewall.md) als uw organisatie een proxyserver of firewall gebruikt, zodat de agents kunnen communiceren met de Hallo Log Analytics-service.
