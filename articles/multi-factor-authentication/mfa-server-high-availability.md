---
title: aaaConfigure Azure MFA-Server voor hoge beschikbaarheid | Microsoft Docs
description: Implementeer meerdere exemplaren van Azure multi-factor Authentication-Server in de configuraties die maximale beschikbaarheid.
services: multi-factor-authentication
keywords: Azure MFA
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>Azure multi-factor Authentication-Server configureren voor hoge beschikbaarheid

tooachieve hoge beschikbaarheid met uw Azure-Server MFA-implementatie, moet u toodeploy meerdere MFA-servers. Deze sectie bevat informatie over een tooachieve taakverdeling ontwerp uw doelen voor hoge beschikbaarheid in uw Azure MFS Server-implementatie.

## <a name="mfa-server-overview"></a>Overzicht van de MFA-Server

Hallo architectuur van de service Azure MFA-Server omvat diverse onderdelen, zoals wordt weergegeven in het volgende diagram Hallo:

 ![Architectuur van MFA-Server](./media/mfa-server-high-availability/mfa-ha-architecture.png)

Een MFA-Server is een Windows-Server die hello Azure multi-factor Authentication software is geïnstalleerd. Hallo MFA-Server-exemplaar moet worden geactiveerd door Hallo MFA-Service in Azure toofunction. Meer dan één MFA-Server worden geïnstalleerd op lokale.

Hallo eerste MFA-Server die is geïnstalleerd, is Hallo master MFA-Server bij de activering door hello Azure MFA-Service standaard. Hallo master MFA-server heeft een beschrijfbare kopie van Hallo PhoneFactor.pfdata database. Volgende installaties van exemplaren van MFA-Server worden slaves genoemd. Hallo MFA slaves hebben een gerepliceerde alleen-lezen kopie van Hallo PhoneFactor.pfdata database. MFA servers repliceren gegevens door middel van Remote Procedure Call (RPC). Alle servers van MFA moet gezamenlijk zijn verbonden met het domein of zelfstandige tooreplicate informatie.

MFA master en slave MFA-Servers communiceren met Hallo MFA-Service wanneer tweeledige verificatie vereist is. Bijvoorbeeld, wanneer een gebruiker toogain toegang tooan toepassing waarvoor tweeledige verificatie probeert, Hallo gebruiker eerst geverifieerd door een id-provider, zoals Active Directory (AD).

Na een geslaagde authenticatie met AD Hallo MFA-Server communiceert met de Hallo MFA-Service. Hallo MFA-Server wacht op een melding van Hallo MFA-Service tooallow of weigeren van toegang Hallo-toohello gebruikerstoepassing.

Als master Hallo MFA-server offline gaat, verificaties nog steeds kunnen worden verwerkt, maar bewerkingen waarvoor wijzigingen toohello MFA database kunnen niet worden verwerkt. (Voorbeelden zijn: het toevoegen van gebruikers, selfservice PINCODE wijzigen en het wijzigen van gebruikersgegevens Hallo)

## <a name="deployment"></a>Implementatie

Houd rekening met Hallo belangrijke punten voor taakverdeling Azure MFA-Server en de bijbehorende onderdelen te volgen.

* **Met behulp van RADIUS-standaard tooachieve hoge beschikbaarheid**. Als u van Azure MFA-Servers als RADIUS-servers gebruikmaakt, kunt u mogelijk een MFA-Server configureren als een RADIUS-doel voor primaire verificatie en andere Azure MFA-Servers als secundaire verificatie doelen. Deze methode tooachieve hoge beschikbaarheid kan echter niet zijn praktische omdat u wachten voor een periode toooccur time moet-verificatie is mislukt op de primaire verificatiedoel Hallo voordat u tegen Hallo secundaire verificatie kan worden geverifieerd het doel. Het is efficiënter tooload saldo Hallo RADIUS-verkeer tussen Hallo RADIUS-client en Hallo RADIUS-Servers (in dit geval hello Azure MFA-Servers die fungeren als RADIUS-servers) zodat u Hallo RADIUS-clients met één URL van een die ze configureren kunt naar kunnen verwijzen.
* **Moet promoveren toomanually MFA slaves**. Hallo master Azure MFA-server offline gaat, blijven hello secundaire Servers van de Azure MFA tooprocess MFA aanvragen. Echter totdat een master MFA-server beschikbaar is, beheerders kunnen geen gebruikers toevoegen of MFA-instellingen wijzigen en kunnen gebruikers niet met behulp van de gebruikersportal Hallo wijzigingen aanbrengen. Promoveren van een MFA slave toohello master-functie is altijd een handmatig proces.
* **Afscheidbaarheid van onderdelen**. Azure MFA-Server bestaat uit verschillende onderdelen die kunnen worden geïnstalleerd op Hallo Hallo hetzelfde exemplaar van WindowsServer of op verschillende exemplaren. Deze onderdelen zijn Hallo Gebruikersportal webservice voor mobiele App en Hallo AD FS-adapter (agent). Deze Afscheidbaarheid maakt het mogelijk toouse Hallo Web Application Proxy toopublish hello Gebruikersportal- en Mobile App Web Server uit het perimeternetwerk Hallo. Een dergelijke configuratie voegt toohello algehele beveiliging van uw ontwerp, zoals wordt weergegeven in het volgende diagram Hallo. Hello MFA User Portal- en Mobile App Web Server kan ook worden geïmplementeerd in HA taakverdeling configuraties.

   ![MFA-Server met een perimeternetwerk](./media/mfa-server-high-availability/mfasecurity.png)

* **Eenmalig wachtwoord (OTP) via SMS (aka eenzijdige SMS) vereist Hallo gebruik van een tijdelijke sessies als verkeer taakverdeling**. SMS in één richting is een verificatieoptie die ervoor zorgt dat Hallo MFA-Server toosend Hallo gebruikers een tekstbericht met een OTP. Hallo gebruiker voert Hallo OTP in een promptvenster toocomplete Hallo MFA uitdaging. Als u taakverdeling van Azure MFA-Servers, moet hello dezelfde server die de eerste authenticatie-aanvraag Hallo behandeld Hallo-server waarop OTP het Hallo-bericht van gebruiker Hallo ontvangen; Als een andere MFA-Server Hallo OTP antwoord ontvangt, wordt Hallo verificatievraag mislukt. Zie voor meer informatie [één keer wachtwoord via SMS toegevoegd tooAzure MFA-Server](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server).
* **Taakverdeling implementaties van Hallo Gebruikersportal en de webservice voor mobiele App moet een tijdelijke sessies**. Als u load balancing Hallo MFA User Portal en Hallo webservice voor mobiele App, elke sessie moet toostay op Hallo dezelfde server.

## <a name="high-availability-deployment"></a>Hoge beschikbaarheid-implementatie

Hallo toont volgende diagram een volledige op HA taakverdeling implementatie van Azure MFA en de bijbehorende onderdelen, samen met ADFS ter referentie.

 ![Azure MFA-Server HA-implementatie](./media/mfa-server-high-availability/mfa-ha-deployment.png)

Houd er rekening mee Hallo volgende items voor Hallo navenant genummerd gebied Hallo voorgaande diagram.

1. Hallo twee Azure MFA-Servers (MFA1 en MFA2) zijn geladen taakverdeling (mfaapp.contoso.com) en zijn geconfigureerde toouse een statische poort (4443) tooreplicate hello PhoneFactor.pfdata database. Hallo Web Service SDK is geïnstalleerd op elk van de Hallo MFA-Server tooenable communicatie via TCP-poort 443 met Hallo ADFS-servers. Hallo MFA servers worden geïmplementeerd in een stateless configuratie van taakverdeling. Echter, als u OTP toouse via SMS wilde, moet u stateful taakverdeling.
   ![Azure MFA-Server - appserver HA](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > Omdat de RPC dynamische poorten gebruikt, zijn het wordt niet aangeraden tooopen firewalls up toohello bereik van dynamische poorten die RPC kan gebruiken. Als u een firewall hebt **tussen** uw MFA-toepassingsservers, moet u configureren Hallo MFA-Server toocommunicate op een statische poort voor Hallo replicatieverkeer tussen servers slave en master en deze te openen die poort op uw firewall. U kunt statische poort Hallo afdwingen door het maken van een DWORD-registerwaarde op ```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor``` aangeroepen ```Pfsvc_ncan_ip_tcp_port``` en instellingswaarde Hallo tooan beschikbare statische poort. Verbindingen zijn altijd wordt geïnitieerd door Hallo slave MFA Servers toohello master, Hallo statische poort is alleen vereist op Hallo master, maar omdat op elk gewenst moment u een lager niveau bevindende toobe Hallo model promoveren kunt, moet u Hallo statische poort instellen op alle Servers met MFA.

2. Hallo twee gebruiker Portal/MFA mobiele App servers (MFA-UP-MAS1 en MFA-UP-MAS2) worden verdeeld een **stateful** configuration (mfa.contoso.com). Intrekken dat een tijdelijke sessies zijn vereist voor de load balancer Hallo MFA User Portal en de mobiele App Service.
   ![Azure MFA-Server - Gebruikersportal en de mobiele App Service HA](./media/mfa-server-high-availability/mfaportal.png)
3. Hallo ADFS-Server-farm is load balanced en toohello Internet via AD FS-proxy's Netwerktaakverdeling in het perimeternetwerk Hallo gepubliceerd. Elke AD FS-Server gebruikt Hallo ADFS agent toocommunicate Hello Azure MFA-Servers via één taakverdeling URL (mfaapp.contoso.com) via TCP-poort 443.

## <a name="next-steps"></a>Volgende stappen

* [Azure MFA-Server installeren en configureren](multi-factor-authentication-get-started-server.md)
