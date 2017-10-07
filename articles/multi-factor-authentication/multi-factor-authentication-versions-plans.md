---
title: aaaAzure MFA-versies en het verbruik van plannen | Microsoft Docs
description: Informatie over Hallo multi-factor Authentication-client en Hallo verschillende methoden en versies die beschikbaar zijn. Meer informatie over elk plan verbruik
keywords: 
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
editor: yossib
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: kgremban
ms.openlocfilehash: 4914747e435531b9f950356d23aa386f3d9585d2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-azure-multi-factor-authentication"></a>Hoe tooget Azure multi-factor Authentication

Wanneer deze wordt gezet tooprotecting uw accounts, moet verificatie in twee stappen standaard in uw organisatie. Deze functie is vooral belangrijk voor beheerdersaccounts met toegang tooresources uitgebreide. Microsoft biedt daarom basic in twee stappen verificatie functies tooOffice 365 en Azure beheerders. Als u tooupgrade Hallo functies wilt gebruiken voor uw beheerders of in twee stappen verificatie toohello rest van uw gebruikers uitbreiden, kunt u Azure multi-factor Authentication kunt aanschaffen. 

Dit artikel behandelt Hallo verschil tussen het Hallo-versies die worden aangeboden tooadministrators en Hallo volledige Azure MFA-versie wordt uitgelegd en geeft aan welke functies beschikbaar zijn in elk zijn. Als u klaar bent wordt toodeploy hello Azure MFA-aanbieding is voltooid, Hallo latere secties dekt implementatie-opties en hoe Microsoft verbruik berekent.

>[!IMPORTANT]
>In dit artikel is bedoeld toobe een handleiding toohelp dat u begrijpt Hallo verschillende manieren toobuy Azure multi-factor Authentication. Voor specifieke informatie over prijzen en facturering, raadpleegt u altijd toohello [multi-factor Authentication-pagina met prijzen](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

## <a name="available-versions-of-azure-multi-factor-authentication"></a>Beschikbare versies van Azure multi-factor Authentication

Hallo staan volgende tabel Hallo verschillen tussen de drie versies van multi-factor authentication-server:

| Versie | Beschrijving |
| --- | --- |
| Multi-factor Authentication voor Office 365 |Deze versie werkt alleen met Office 365-toepassingen en wordt beheerd via Hallo Office 365-portal. Beheerders kunnen [Office 365-resources met verificatie in twee stappen beveiligen](https://support.office.com/article/Set-up-multi-factor-authentication-for-Office-365-users-8f0454b2-f51a-4d9c-bcde-2c48e41621c6). Deze versie is onderdeel van een Office 365-abonnement. |
| Multi-factor Authentication voor Azure-beheerders | Globale beheerders van Azure tenants kunnen inschakelen verificatie in twee stappen voor de globale beheerdersaccounts zonder extra kosten.|
| Azure Multi-Factor Authentication | Vaak waarnaar wordt verwezen tooas Hallo 'volledige' versie, Azure multi-factor Authentication biedt Hallo allerbeste set mogelijkheden. Biedt extra configuratieopties via Hallo [klassieke Azure-portal](https://manage.windowsazure.com)geavanceerde rapportage en ondersteuning voor een bereik van lokale en cloudtoepassingen. Azure multi-factor Authentication is opgenomen in Azure Active Directory Premium (P1 en P2 plannen) en Enterprise Mobility + Security (E3 en E5 plannen) en kan worden geïmplementeerd op een [in Hallo cloud of on-premises](multi-factor-authentication-get-started.md). |

## <a name="feature-comparison-of-versions"></a>Vergelijking van functies van versies
Hallo volgende tabel bevat een lijst met Hallo-functies die beschikbaar in Hallo zijn verschillende versies van Azure multi-factor Authentication.

> [!NOTE]
> Deze Vergelijkingstabel komen aan bod Hallo-functies die deel uitmaken van elke versie van multi-factor Authentication. Als u de volledige Azure multi-factor Authentication-service Hallo hebt, sommige functies mogelijk niet beschikbaar, afhankelijk van of u gebruiken [MFA in de cloud Hallo of MFA lokale](multi-factor-authentication-get-started.md).


| Functie | Multi-factor Authentication voor Office 365 | Multi-factor Authentication voor Azure-beheerders | Azure Multi-Factor Authentication |
| --- |:---:|:---:|:---:|
| Beveiligen van beheerdersaccounts met MFA |● |● (alleen globale beheerdersaccounts) |● |
| Mobiele app als een tweede factor |● |● |● |
| Telefoonoproep als tweede factor |● |● |● |
| SMS als tweede factor |● |● |● |
| App-wachtwoorden voor clients die geen ondersteuning voor MFA bieden |● |● |● |
| Beheerdercontrole over verificatiemethoden |● |● |● |
| Pincodemodus | | |● |
| Fraudewaarschuwing | | |● |
| MFA-rapporten | | |● |
| Eenmalige toegang | | |● |
| Aangepaste begroeting voor telefoongesprekken | | |● |
| Aangepaste Nummerweergave voor telefoongesprekken | | |● |
| Goedgekeurde IP-adressen | | |● |
| MFA herinneren voor vertrouwde apparaten |● |● |● |
| MFA SDK | | |● (vereist multi-factor Authentication-provider en volledige Azure-abonnement) |
| MFA voor on-premises toepassingen | | |● |

## <a name="how-tooget-azure-multi-factor-authentication"></a>Hoe tooget Azure multi-factor Authentication
Als u Hallo volledige functionaliteit van Azure multi-factor Authentication wilt, zijn er verschillende opties:

### <a name="option-1---mfa-licenses"></a>Optie 1: MFA licenties

Azure multi-factor Authentication-licenties koopt en toewijzen tooyour gebruikers in Azure Active Directory. 

Als u deze optie gebruikt, moet u een Azure multi-factor Authentication-Provider maken alleen als u moet ook de verificatie in twee stappen tooprovide voor gebruikers die geen licenties hebt. Anders wordt u mogelijk worden gefactureerd twee keer.

### <a name="option-2---bundled-licenses-that-include-mfa"></a>Optie 2 - gebundeld licenties met MFA

Licenties die hieraan tooyour gebruikers in Azure Active Directory en Azure multi-factor Authentication, zoals Azure Active Directory Premium (P1 of P2) of Enterprise Mobility + Security (E3 of E5) bevatten. 

Als u deze optie gebruikt, moet u een Azure multi-factor Authentication-Provider maken alleen als u moet ook de verificatie in twee stappen tooprovide voor gebruikers die geen licenties hebt. Anders wordt u mogelijk worden gefactureerd twee keer. 

### <a name="option-3---mfa-consumption-based-model"></a>Optie 3: MFA-model op basis van verbruik

Een Azure multi-factor Authentication-Provider binnen een Azure-abonnement maken. Azure MFA-Providers zijn Azure-resources worden gefactureerd op basis van uw Enterprise Agreement, Azure maandbedrag of creditcard net als alle andere Azure-resources. Deze providers kunnen alleen worden gemaakt in de volledige Azure-abonnementen niet beperkt Azure-abonnementen waarvoor een $-0 uitgavenlimiet. Beperkte abonnementen worden gemaakt wanneer u licenties, zoals in opties 1 en 2 activeert. 

Wanneer u een Azure multi-factor Authentication-Provider gebruikt, zijn er twee modellen beschikbaar die via uw Azure-abonnement worden gefactureerd:  

1. **Per gebruiker** - voor ondernemingen die u wilt dat verificatie van tooenable in twee stappen voor een vast aantal werknemers die regelmatig dienen te worden geverifieerd. Facturering per gebruiker is gebaseerd op Hallo aantal gebruikers dat is ingeschakeld voor MFA in uw Azure AD-tenant en/of Azure MFA-Server. Als gebruikers zijn ingeschakeld voor MFA in beide Azure AD en Azure MFA-Server en domein sync (Azure AD Connect) is ingeschakeld, moet we tellen Hallo grotere set van gebruikers. Als synchronisatie van domein is niet ingeschakeld, wordt er Hallo som van alle gebruikers die zijn ingeschakeld voor MFA in Azure AD tellen en Azure MFA-Server. Facturering is dagelijks naar rato en gerapporteerde toohello Commerce-systeem. 

  > [!NOTE]
  > Facturering voorbeeld 1: U hebt 5000 gebruikers die zijn ingeschakeld voor MFA vandaag. Hallo MFA system verdeelt dat nummer door 31 en 161.29 gebruikers rapporten voor die dag. Morgen schakelt u 15 meer gebruikers, zodat Hallo MFA system 161.77 gebruikers voor die dag rapporten. Totaal aantal gebruikers kosten in rekening gebracht op basis van uw Azure-abonnement Hallo opgeteld tooaround 5.000 door Hallo van Hallo cyclus facturering. 
  >
  > Facturering voorbeeld 2: U hebt een mengeling van gebruikers met licenties en gebruikers zonder, zodat u een per gebruiker Azure MFA-Provider toomake up Hallo verschil hebt. Er zijn 4.500 Enterprise Mobility + Security-licenties op uw tenant, maar 5000 gebruikers die zijn ingeschakeld voor MFA. Uw Azure-abonnement wordt gefactureerd voor 500 gebruikers, naar rato en dagelijks gerapporteerd als 16.13 gebruikers. 

2. **Per verificatie** - voor ondernemingen die u wilt dat de verificatie in twee stappen tooenable voor een grote groep met gebruikers hoeven minder vaak verificatie. Facturering is gebaseerd op Hallo aantal in twee stappen verificatie aanvragen ontvangen door hello Azure MFA-cloudservice, ongeacht of deze verificaties slagen of geweigerd. Deze facturering wordt weergegeven op uw van Azure-gebruiksinstructie in de packs van 10 verificaties en gerapporteerde toohello Commerce system dagelijks. 

  > [!NOTE]
  > Facturering voorbeeld 3: vandaag de dag hello Azure MFA-service ontvangen 3,105 aanvragen voor de verificatie in twee stappen. Uw Azure-abonnement wordt gefactureerd voor 310.5 verificatie packs. 

Het is belangrijk toonote dat u kunt Azure MFA-licenties hebt, maar nog steeds in rekening voor de configuratie op basis van verbruik gebracht ophalen. Als u een per authenticatie Azure MFA-Provider hebt ingesteld, wordt u gefactureerd voor elke aanvraag van de verificatie in twee stappen ook als deze door gebruikers die licenties hebt gedaan. Als u een Azure MFA-Provider per gebruiker ingesteld op een domein dat geen gekoppelde tooyour Azure AD-tenant, wordt u gefactureerd per ingeschakelde gebruiker zelfs als de gebruikers met licenties in Azure AD. 

## <a name="next-steps"></a>Volgende stappen

- Zie voor meer prijsinformatie [prijzen van Azure MFA](https://azure.microsoft.com/pricing/details/multi-factor-authentication/).

- Kies of toodeploy Azure MFA [in Hallo cloud of on-premises](multi-factor-authentication-get-started.md)
