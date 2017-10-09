---
title: aaaSecuring toegang tooAzure RemoteApp, en ook buiten | Microsoft Docs
description: Meer informatie over hoe veilig toegang tooAzure RemoteApp met behulp van voorwaardelijke toegang in Azure Active Directory
services: remoteapp
documentationcenter: 
author: piotrci
manager: mbaldwin
ms.assetid: a19b0b09-ab26-4beb-80bb-33a46da39887
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 98dfe69e2f5fa5014b6eb3157e01f131c287134d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="securing-access-tooazure-remoteapp-and-beyond"></a>Toegang tooAzure RemoteApp, beveiligen en hoger
> [!IMPORTANT]
> Azure RemoteApp wordt op 31 augustus 2017 buiten gebruik gesteld. Lees Hallo [aankondiging](https://go.microsoft.com/fwlink/?linkid=821148) voor meer informatie.
> 
> 

In dit artikel krijgt we een overzicht van hoe een beheerder een kanaal voor veilige toegang vanaf de eindgebruiker Hallo via Azure RemoteApp en eindigend met een beveiligde bron, zoals een SQL-database of een andere toepassing back-end kunt instellen. Hallo-doel is toomake ervoor dat alleen geautoriseerde gebruikers vergadering Hallo gewenst voorwaarden toegang tot externe toepassingen en die beveiligde back-end Hallo kunnen alleen worden benaderd vanuit Hallo beheerd Azure RemoteApp-omgeving en niet vanuit andere locaties.

Er zijn 3 belangrijke gebieden Hallo beheerder moet toolook op:

![Overwegingen met betrekking tot Azure RemoteApp-voorwaardelijke toegang](./media/remoteapp-secureaccess/ra-conditionalenvironment.png)

Lees verder voor informatie en antwoorden toothese vragen.

## <a name="who-can-access-hello-collection"></a>Wie toegang heeft tot de verzameling Hallo?
Hallo beheerder eenmaal heeft gekozen Hallo-gebruikers die toegang externe toepassingen in Hallo-verzameling tot. U kunt Azure Active Directory (Azure AD) werk of schoolaccounts (eerder genoemd, 'organisatieaccounts') of Microsoft-accounts (bijvoorbeeld @outlook.com). De meeste zakelijke scenario's Azure AD-accounts; gebruiken Deze kunnen u gebruikmaken van de functies van voorwaardelijke toegang verderop besproken en zijn ook Hallo alleen keuze voor domein-verzamelingen. Hallo rest van Hallo artikel wordt ervan uitgegaan dat u gebruikmaakt van Azure AD-accounts met Azure RemoteApp.

**Wat we hebben bereikt:**

Met behulp van Azure AD-accounts toocontrol toegang tooAzure die RemoteApp ons twee dingen biedt:

1. We weten altijd wie toegang heeft tot toepassingen we hebt gepubliceerd en hebben toegang tot back-ends voor deze toepassingen verbinding met maken Hallo.
2. We bepalen hello Azure AD onderliggende zodat we maken kunt en verwijderen gebruikersaccounts, set wachtwoordbeleid, gebruik van meervoudige verificatie, enzovoort. 

## <a name="how-is-hello-collection-accessed-from-where"></a>Hoe wordt de verzameling Hallo geopend Waar?
Beheerders willen vaak toodefine beleidsregels voor toegang tot een openbare internetgerichte-omgeving, zoals Azure RemoteApp. Bijvoorbeeld, willen ze dat gebruikers toegang hebben tot Hallo-omgeving van buiten het bedrijfsnetwerk Hallo beschikken over toouse multi-factor authentication (MFA) toogain; tooensure of misschien deze volledig moeten worden geblokkeerd.

Azure RemoteApp-beheerders kunnen Hallo-functionaliteit is beschikbaar via beleid voor voorwaardelijke toegang van Azure AD Premium tooset gebruiken voor hun Azure RemoteApp-omgeving. Ze kunnen ook gebruiken uitgebreide rapportage en waarschuwen functies toomonitor hoe Hallo-omgeving wordt geopend.

### <a name="how-tooset-up-conditional-access-for-azure-remoteapp"></a>Hoe tooset van voorwaardelijke toegang voor Azure RemoteApp
We gaan toowalk via een voorbeeldscenario zijn – hello Azure RemoteApp beheerder wil tooblock access toohello omgeving wanneer gebruikers zich buiten het bedrijfsnetwerk Hallo.

> [!NOTE]
> Er wordt ervan uitgegaan dat u een upgrade hebt uitgevoerd op toohello Azure AD Premium-laag en dat u ten minste één Azure RemoteApp-verzameling hebt gemaakt.
> 
> 

1. Klik in de Azure-portal op Hallo **Active Directory** tabblad. Klik vervolgens op Hallo map waarin u tooconfigure.
   
   Onthouden: Voorwaardelijke toegang is een eigenschap van uw directory en niet van Azure RemoteApp, zodat alle configuratie wordt uitgevoerd op Hallo directory niveau. Dit betekent ook dat u deze wijzigingen toobe Hallo directory-beheerder toomake nodig.
2. Klik op **toepassingen**, en klik vervolgens op **Microsoft Azure RemoteApp** tooset van voorwaardelijke toegang. Houd er rekening mee dat u voorwaardelijke toegang voor elke toepassing 'software as a service' in uw directory afzonderlijk instellen kunt.
   ![Voorwaardelijke toegang instellen voor Azure RemoteApp](./media/remoteapp-secureaccess/ra-conditionalaccessscreen.png)
3. Op Hallo **configureren** tabblad, stelt u **toegangsregels inschakelen** tooON.
   ![Regels voor toegang inschakelen voor Azure RemoteApp](./media/remoteapp-secureaccess/ra-enableaccessrules.png)
4. U kunt nu verschillende regels configureren en kiezen wie tooapply zodat worden:
   
   1. Kies **blokkeren van toegang niet op het werk** toocompletely wordt voorkomen dat gebruikers toegang hebben tot Azure RemoteApp buiten Hallo-netwerkomgeving die u opgeeft.
   2. Klik op de optie Hallo hieronder toodefine Hallo IP-adresbereiken die deel uitmaken van uw 'vertrouwd netwerk'. Alles buiten die worden geweigerd.
5. Configuratie van de testen door het starten van hello Azure RemoteApp-client van een IP-adres buiten Hallo dat die u hebt opgegeven. Nadat u zich met uw Azure AD-referenties aanmelden ziet u een bericht als volgt:

![Toegang geweigerd tooAzure RemoteApp](./media/remoteapp-secureaccess/ra-accessdenied.png)

### <a name="future-conditional-access-features"></a>Functies voor toekomstige voorwaardelijke toegang
Hello Azure Active Directory-team werkt aan de nieuwe mogelijkheden in voorwaardelijke toegang. Beheerders zijn kunnen toocreate nieuwe typen regels buiten de netwerk locatie op basis van regels. Een openbare preview van nieuwe functionaliteit Hallo moet binnenkort beschikbaar.

### <a name="how-toomonitor-access-tooazure-remoteapp"></a>Hoe toomonitor toegang krijgen tot tooAzure RemoteApp
Een goede functie toouse samen met voorwaardelijke toegang is hello Azure Active Directory Premium rapportagefunctionaliteit. U kunt rapporten toomonitor wie toegang heeft tot uw omgeving gebruiken en verdachte activiteiten detecteren.

Bijvoorbeeld, ziet u Hallo namen van Hallo-gebruikers die Azure RemoteApp, hoe vaak ze het heeft geopend en wanneer.

1. Klik in de Azure-portal op **Active Directory**, en klik vervolgens op uw directory.
2. Ga toohello **rapporten** tabblad.
3. Selecteer in de lijst met rapporten Hallo **toepassingsgebruik** onder **geïntegreerde toepassingen**.
   
   U ziet enkele samengevoegde statistieken voor Azure RemoteApp. 
   ![Samengevoegde statistieken voor Azure RemoteApp-toegang](./media/remoteapp-secureaccess/ra-accessstats.png)
4. Klik op Hallo toepassing tooreveal informatie over gebruikers die toegang tot Azure RemoteApp.
   ![Statistieken van de gebruiker toegang voor Azure RemoteApp](./media/remoteapp-secureaccess/ra-userstats.png)

### <a name="summary"></a>Samenvatting
U kunt met Azure Active Directory Premium toegang regels tooAzure RemoteApp (en andere software als een servicetoepassingen die beschikbaar zijn via Azure AD) instellen. Regels zijn momenteel beperkt toonetwork locatie op basis van beleid, maar wordt in toekomstige Hallo uitgebreid tooother aspecten van enterprise-beheer.

Azure AD Premium biedt ook reporting en bewakingsmogelijkheden die verder Hallo besturingselement Hallo beheerder uitbreiden heeft via de Azure RemoteApp-omgeving.

## <a name="how-do-i-make-sure-my-secure-resource-is-accessible-only-from-my-azure-remoteapp-environment"></a>Hoe maak ik ervoor dat mijn beveiligde resource is alleen toegankelijk vanuit Mijn Azure RemoteApp-omgeving?
In vorige gedeelten van dit artikel gericht we over het beveiligen van toegang toohello Azure RemoteApp-omgeving. We hebben die bereikt in kiezen Hallo-gebruikers die toegang hebben en het instellen van toegangsbeheer regels toofurther hoe ze Hallo service kunnen gebruiken.

Een veelvoorkomend scenario voor implementaties van Azure RemoteApp is dat externe toepassingen Hallo toocommunicate met een back-end-resource, bijvoorbeeld een SQL-database moeten. Deze bron wordt gehost on-premises (bijvoorbeeld in een bedrijfsnetwerk) of in de cloud hello (bijvoorbeeld in Azure IaaS). Beheerders willen vaak toomake ervoor Hallo back-end resource kan alleen worden benaderd door toepassingen die zijn geïmplementeerd via Azure RemoteApp en niet bijvoorbeeld door een toepassing uitvoeren rechtstreeks op de PC van een gebruiker en toegang tot via openbaar Internet. Azure RemoteApp is vaak gezien als Hallo centraal beheerd en beveiligde omgeving en dus de enige pad Hallo via welke gebruikers met communiceren moeten Hallo back-end-resource.

Hallo-oplossing is tooplace beide hello Azure RemoteApp-omgeving en beveiligde bronnen in Hallo Hallo dezelfde Azure Virtual Network (VNET). Als Hallo resource in een andere site, kunt u een site-naar-site VPN-verbinding, bijvoorbeeld een VNet spanning hello Azure-Datacenter toocreate en Hallo klant on-premises omgeving kunt maken.

Azure RemoteApp ondersteunt twee typen implementaties van de verzameling waarin u uw eigen VNET kunt opgeven:

* Niet-domein: Hallo toepassingen hebben 'onbelemmerd zicht' Hallo andere bronnen in Hallo VNET. Dit kan bijvoorbeeld gebruikte tooconnect toepassingen tooa SQL-database die gebruikmaakt van SQL-verificatie zijn (Hallo gebruiker rechtstreeks op Hallo database toepassingen verifiëren)
* Domein: Hallo virtuele machines die worden gebruikt door Azure RemoteApp zijn voor de domeincontroller lid tooa in Hallo VNET. Dit is handig wanneer Hallo toepassingen tooauthenticate op basis van een Windows-domeincontroller in volgorde tooget toegang tooa back-end-bron moeten.
  ![Een verzameling domein in Azure RemoteApp](./media/remoteapp-secureaccess/ra-domainjoined.png)

### <a name="how-toocreate-a-secure-connection-between-azure-and-my-on-premises-environment"></a>Hoe toocreate een beveiligde verbinding tussen Azure en mijn on-premises-omgeving
Er zijn verschillende configuratieopties voor het verbinden van uw Azure- en on-premises omgevingen. Een goed overzicht van opties Hallo is hier beschikbaar.

Met Azure RemoteApp tooconfigure eerst uw VNet nodig en vervolgens worden gebruikt tijdens het proces voor het maken van uw verzameling Hallo. 

## <a name="hello-complete-solution"></a>de volledige oplossing Hallo
Hallo ziet hieronder u de volledige oplossing Hallo waar we een kanaal voor beveiligde toegang van eindgebruiker hello, via Azure RemoteApp (ARA), zijn ingebouwd in Hallo back-end-resource.
![Beveiligen van Azure RemoteApp](./media/remoteapp-secureaccess/ra-secureoverview.png) In stap 1 we Hallo gebruikers geselecteerd en toegangsregels die bepalen hoe ARA toegankelijk zijn gemaakt. In onderstaand voorbeeld voor Hallo toestaan we alleen toegang voor gebruikers die werken met het bedrijfsnetwerk Hallo. Niet-compatibel gebruikers zich niet kunnen tooaccess Hallo ARA-omgeving op alle.
In de fase 2 hebben we Hallo back-end resource alleen via Hallo VNet/VPN-configuratie die we controleren zichtbaar. Azure RemoteApp is geplaatst in Hallo hetzelfde VNet. Hallo-eindresultaat is Hallo resource kan alleen worden benaderd via Hallo ARA-omgeving.

