---
title: aaaManage rollen en gebruikers in Azure Analysis Services-database | Microsoft Docs
description: Meer informatie over hoe toomanage rollen en gebruikers op een Analysis Services-server in Azure-database.
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 2ad069a6bcce11bc43347625cb32ec400d48af18
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="manage-database-roles-and-users"></a>Databaserollen en gebruikers beheren

Op databaseniveau Hallo-model, moeten alle gebruikers tooa rol behoren. Gebruikers met bepaalde machtigingen voor de modeldatabase Hallo definiëren rollen Een gebruiker of beveiligingsgroep groep toegevoegd tooa rol moet een account in een Azure AD-tenant in Hallo hebben hetzelfde abonnement als Hallo-server.

Andere afhankelijk van Hallo hulpprogramma waarmee u hoe u rollen definiëren is, maar Hallo effect is dezelfde Hallo.

Rolmachtigingen zijn onder andere:
*  **Beheerder** -gebruikers volledige machtigingen voor Hallo database hebben. Databaserollen met Administrator-machtigingen zijn anders dan serverbeheerders.
*  **Proces** -gebruikers verbinding kunnen maken van tooand proces bewerkingen uitvoeren op database Hallo en analyseren van gegevens van de database model.
*  **Lees** -gebruikers kunnen gebruiken een client toepassing tooconnect tooand analyseren modelgegevens van de database.

Wanneer een model in tabelvorm-project maakt, kunt u rollen maken en gebruikers of groepen toothose functies toevoegen met rolbeheer in SSDT. Wanneer geïmplementeerde tooa server kunt u gebruiken om SSMS, [Analysis Services-PowerShell-cmdlets](https://msdn.microsoft.com/library/hh758425.aspx), of [Tabellaire Model scripttaal](https://msdn.microsoft.com/library/mt614797.aspx) tooadd (TMSL) of verwijderen van rollen en leden van de gebruiker.

## <a name="tooadd-or-manage-roles-and-users-in-ssdt"></a>tooadd of beheren van rollen en gebruikers in SSDT  
  
1.  In SSDT > **Tabellaire Model Explorer**, met de rechtermuisknop op **rollen**.  
  
2.  Klik in **Role Manager** op **New**.  
  
3.  Typ een naam voor de rol Hallo.  
  
     Standaard wordt Hallo-naam van Hallo standaardrol incrementeel genummerd voor elke nieuwe rol. Het raadzaam typt u een naam die duidelijk aangeeft Hallo lidtype, bijvoorbeeld Financiën Managers of specialisten Human Resources.  
  
4.  Selecteer een van de volgende machtigingen Hallo:  
  
    |Machtiging|Beschrijving|  
    |----------------|-----------------|  
    |**Geen**|Leden Hallo modelschema kunnen niet worden gewijzigd en kunnen gegevens niet opvragen.|  
    |**Lezen**|Leden kunnen een query over gegevens (op basis van rijfilters) maar Hallo modelschema niet wijzigen.|  
    |**Lees- en**|Leden query gegevens (op basis van rijniveau filters) en voer proces en proces alle bewerkingen, maar kunnen het modelschema Hallo niet wijzigen.|  
    |**Proces**|Leden kunnen proces en proces alle bewerkingen uitvoeren. Hallo modelschema kan niet worden gewijzigd en kan gegevens niet opvragen.|  
    |**Beheerder**|Leden kunnen Hallo modelschema wijzigen en alle gegevens opvragen.|   
  
5.  Als het Hallo-rol zijn maken heeft lees- of de machtigingen lezen en proces, kunt u rijfilters toevoegen met behulp van een DAX-formule. Klik op Hallo **rijfilters** tabblad Selecteer een tabel vervolgens, klikt u op Hallo **DAX-Filter** veld en typ vervolgens een DAX-formule.
  
6.  Klik op **leden** > **extern toevoegen**.  
  
8.  In **extern lid toevoegen**, gebruikers of groepen opgeven in uw Azure AD-tenant op e-mailadres. Nadat u op OK en rolbeheer sluit, rollen en leden van een rol worden weergegeven in de Tabellaire Model Explorer. 
 
     ![Rollen en gebruikers in de Tabellaire Model Explorer](./media/analysis-services-database-users/aas-roles-tmexplorer.png)

9. Tooyour Azure Analysis Services-server implementeren.


## <a name="tooadd-or-manage-roles-and-users-in-ssms"></a>tooadd of beheren van rollen en gebruikers in SSMS
tooadd rollen en gebruikers tooa modeldatabase geïmplementeerd, moet u de server verbonden toohello als serverbeheerder of wordt al een databaserol met administrator-machtigingen.

1. Met de rechtermuisknop in Verkenner-Object, **rollen** > **nieuwe rol**.

2. In **rol maken**, een role-naam en beschrijving opgeven.

3. Selecteer een machtiging.
   |Machtiging|Beschrijving|  
   |----------------|-----------------|  
   |**Volledig beheer (beheerder)**|Leden kunnen wijzigen Hallo modelschema, verwerken en alle gegevens kunt opvragen.| 
   |**Proces-database**|Leden kunnen proces en proces alle bewerkingen uitvoeren. Hallo modelschema kan niet worden gewijzigd en kan gegevens niet opvragen.|  
   |**Lezen**|Leden kunnen een query over gegevens (op basis van rijfilters) maar Hallo modelschema niet wijzigen.|  
  
4. Klik op **lidmaatschap**, voert u een gebruiker of groep in uw Azure AD-tenant op e-mailadres.

     ![Gebruiker toevoegen](./media/analysis-services-database-users/aas-roles-adduser-ssms.png)

5. Als het Hallo-rol die u maakt is de machtiging lezen, kunt u rijfilters toevoegen met behulp van een DAX-formule. Klik op **rijfilters**, selecteer een tabel en typ vervolgens een DAX-formule in Hallo **DAX-Filter** veld. 

## <a name="tooadd-roles-and-users-by-using-a-tmsl-script"></a>tooadd rollen en gebruikers met een script TMSL
U kunt een TMSL-script uitvoeren in Hallo XMLA-venster in SSMS of met behulp van PowerShell. Gebruik Hallo [CreateOrReplace](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-commands/createorreplace-command-tmsl) opdracht en Hallo [rollen](https://docs.microsoft.com/sql/analysis-services/tabular-models-scripting-language-objects/roles-object-tmsl) object.

**Voorbeeldscript TMSL**

In dit voorbeeld wordt een externe gebruiker B2B en een groep toohello analist rol met machtigingen voor lezen voor Hallo SalesBI database toegevoegd. Beide Hallo externe gebruiker en groep moet in dezelfde Azure AD-tenant.

```
{
  "createOrReplace": {
    "object": {
      "database": "SalesBI",
      "role": "Analyst"
    },
    "role": {
      "name": "Users",
      "description": "All allowed users tooquery hello model",
      "modelPermission": "read",
      "members": [
        {
          "memberName": "user1@contoso.com",
          "identityProvider": "AzureAD"
        },
        {
          "memberName": "group1@adventureworks.com",
          "identityProvider": "AzureAD"
        }
      ]
    }
  }
}
```

## <a name="tooadd-roles-and-users-by-using-powershell"></a>tooadd rollen en gebruikers met behulp van PowerShell
Hallo [SqlServer](https://msdn.microsoft.com/library/hh758425.aspx) module biedt taakspecifieke database management-cmdlets en Hallo algemeen Invoke ASCmd cmdlet die een Tabellair Model Scripting Language (TMSL) query of script accepteert. Hallo volgende cmdlets worden gebruikt voor databaserollen en gebruikers beheren.
  
|Cmdlet|Beschrijving|
|------------|-----------------| 
|[Voeg RoleMember](https://msdn.microsoft.com/library/hh510167.aspx)|Toevoegen van een lid tooa-databaserol.| 
|[Verwijder RoleMember](https://msdn.microsoft.com/library/hh510173.aspx)|Een lid verwijderen uit een databaserol.|   
|[Aanroepen ASCmd](https://msdn.microsoft.com/library/hh479579.aspx)|Een script TMSL uitvoeren.|

## <a name="row-filters"></a>Rijfilters  
Rijfilters definiëren welke rijen in een tabel door leden van een bepaalde rol kunnen worden opgevraagd. Rijfilters zijn gedefinieerd voor elke tabel in een model met DAX formules.  
  
Rijfilters alleen voor rollen met lees- en kunnen worden gedefinieerd en proces machtigingen. Standaard, als een rijfilter is niet gedefinieerd voor een bepaalde tabel kunnen leden opvragen alle rijen in de tabel Hallo tenzij cross-filtering is van toepassing van een andere tabel.
  
 Rijfilters vereisen een DAX-formule, die moet worden geëvalueerd tooa TRUE/FALSE-waarde, toodefine Hallo rijen die door leden van die bepaalde rol kunnen worden opgevraagd. Rijen niet opgenomen in Hallo DAX-formule, kunnen niet worden opgevraagd. Tabel Klanten bijvoorbeeld Hallo Hello rij filters expressie, na *= klanten [Country] = "VS"*, klanten in de Verenigde Staten Hallo alleen de leden van de rol van Hallo verkoop kunnen zien.  
  
Rijfilters toepassen toohello opgegeven rijen en de gerelateerde rijen. Wanneer een tabel meerdere relaties heeft, toepassing filters beveiliging voor Hallo-relatie die actief is. Rijfilters beginnen en eindigen met een andere rij filers gedefinieerd voor de gerelateerde tabellen, bijvoorbeeld:  
  
|Tabel|DAX-expressie|  
|-----------|--------------------|  
|Regio|= Regio [Country] = "VS"|  
|ProductCategory|= ProductCategory [Name] = "Fietsen"|  
|Transacties|= Transacties [jaar] = 2016|  
  
 Hallo netto effect is leden gegevensrijen waarbij Hallo klant is in de Verenigde Staten hello, Hallo productcategorie voor fietsen en Hallo jaar voor 2016 kunnen opvragen. Gebruikers kunnen geen transacties buiten de Verenigde Staten hello, transacties die niet fietsen of transacties niet 2016 tenzij ze deel uitmaken van een andere functie die deze machtigingen verleent opvragen.
  
 Hallo-filter, kunt u *=FALSE()*, toodeny toegang tooall rijen voor een hele tabel.

## <a name="next-steps"></a>Volgende stappen
  [Serverbeheerders beheren](analysis-services-server-admins.md)   
  [Azure analyseservices met PowerShell beheren](analysis-services-powershell.md)  
  [Scripting Language (TMSL) Reference Model in tabelvorm](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference)

