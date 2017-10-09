---
title: Dynamische DNS-tooregister hostnamen aaaUsing
description: Deze pagina geeft informatie over hoe tooset van dynamische DNS-tooregister hostnamen in uw eigen DNS-servers.
services: dns
documentationcenter: na
author: GarethBradshawMSFT
manager: timlt
editor: 
ms.assetid: c315961a-fa33-45cf-82b9-4551e70d32dd
ms.service: dns
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/23/2017
ms.author: garbrad
ms.openlocfilehash: 8d4b44265714e6976f26bfb3446e8101aa70996a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="using-dynamic-dns-tooregister-hostnames-in-your-own-dns-server"></a>Gebruik van dynamische DNS-tooregister hostnamen in uw eigen DNS-server
[Azure biedt naamomzetting](virtual-networks-name-resolution-for-vms-and-role-instances.md) voor virtuele machines (VM's) en rolinstanties. Wanneer uw naamomzetting moet verder dan die worden verstrekt door Azure, kunt u uw eigen DNS-servers opgeven. Dit biedt u de DNS-oplossing toosuit power tootailor Hallo uw eigen specifieke behoeften. Bijvoorbeeld, moet u mogelijk tooaccess lokale bronnen via uw Active Directory-domeincontroller.

Wanneer uw aangepaste DNS-servers worden gehost als Azure virtuele machines kunnen worden doorgestuurd hostnaam query's voor Hallo hetzelfde vnet tooAzure tooresolve hostnamen. Als u niet toouse deze route wenst, kunt u uw VM hostnamen in uw DNS-server met behulp van dynamische DNS registreren.  Azure heeft geen Hallo mogelijkheid (bijvoorbeeld referenties) toodirectly records maken in uw DNS-servers, zodat het alternatieve regelingen vaak nodig zijn. Hier volgen enkele algemene scenario's met alternatieven.

## <a name="windows-clients"></a>Windows-clients
Niet-domein Windows-clients proberen onbeveiligde dynamische DNS-(DDNS) updates wanneer ze worden opgestart of wanneer hun IP-adres verandert. Hallo DNS-naam is Hallo hostnaam plus Hallo primaire DNS-achtervoegsel. Azure Hallo primaire DNS-achtervoegsel leeg laat, maar u kunt dit instellen in Hallo VM, via Hallo [UI](https://technet.microsoft.com/library/cc794784.aspx) of [met behulp van automatisering](https://social.technet.microsoft.com/forums/windowsserver/3720415a-6a9a-4bca-aa2a-6df58a1a47d7/change-primary-dns-suffix).

Domein van de Windows-clients voor het registreren van hun IP-adressen met Hallo-domeincontroller met behulp van beveiligde dynamische DNS. Hallo lid van domein proces Hallo primaire DNS-achtervoegsel op Hallo client ingesteld en maakt en onderhoudt Hallo-vertrouwensrelatie.

## <a name="linux-clients"></a>Linux-clients
Linux-clients in het algemeen niet registreren bij Hallo DNS-server bij het opstarten, ze wordt ervan uitgegaan dat Hallo DHCP-server heeft het. Azure DHCP-servers geen Hallo mogelijkheid of referenties tooregister records in uw DNS-server.  U kunt een hulpmiddel *nsupdate*, die is opgenomen in Hallo Bind pakket, toosend dynamische DNS-updates. Aangezien Hallo dynamische DNS-protocol is gestandaardiseerd, kunt u *nsupdate* zelfs wanneer u gebruikt geen binding op Hallo DNS-server.

U kunt Hallo hooks die worden geleverd door Hallo DHCP-client toocreate gebruiken en onderhouden van Hallo hostnaam Hallo DNS-server. Tijdens de cyclus van een DHCP-hello, Hallo-client wordt uitgevoerd Hallo-scripts in */etc/dhcp/dhclient-exit-hooks.d/*. Dit kan zijn tooregister Hallo nieuwe IP-adres gebruikt met behulp van *nsupdate*. Bijvoorbeeld:

        #!/bin/sh
        requireddomain=mydomain.local

        # only execute on hello primary nic
        if [ "$interface" != "eth0" ]
        then
            return
        fi

        # when we have a new IP, perform nsupdate
        if [ "$reason" = BOUND ] || [ "$reason" = RENEW ] ||
           [ "$reason" = REBIND ] || [ "$reason" = REBOOT ]
        then
            host=`hostname`
            nsupdatecmds=/var/tmp/nsupdatecmds
              echo "update delete $host.$requireddomain a" > $nsupdatecmds
              echo "update add $host.$requireddomain 3600 a $new_ip_address" >> $nsupdatecmds
              echo "send" >> $nsupdatecmds

              nsupdate $nsupdatecmds
        fi

        
        

U kunt ook Hallo *nsupdate* opdracht tooperform beveiligde dynamische DNS-updates. Bijvoorbeeld, wanneer u een Bind DNS-server, een openbaar / persoonlijk sleutelpaar is [gegenereerd](http://linux.yyz.us/nsupdate/).  Hallo DNS-server is [geconfigureerd](http://linux.yyz.us/dns/ddns-server.html) met openbare onderdeel Hallo van Hallo sleutel zodat die er het Hallo-handtekening op Hallo aanvraag kunt controleren. Moet u Hallo *-k* optie tooprovide Hallo sleutelpaar-te*nsupdate* om Hallo update dynamische DNS-aanvraag toobe ondertekend.

Wanneer u een Windows-DNS-server gebruikt, kunt u Kerberos-verificatie gebruiken Hello *-g* parameter in *nsupdate* (niet beschikbaar in Windows-versie van Hallo *nsupdate* ). toodo dit, gebruik *kinit* tooload Hallo referenties (bijvoorbeeld van een [keytab-bestand](http://www.itadmintools.com/2011/07/creating-kerberos-keytab-files.html)). Vervolgens *nsupdate -g* Hallo referenties uit de cache Hallo opgehaald.

Indien nodig, kunt u een DNS-zoekopdracht achtervoegsel tooyour VM's kunt toevoegen. Hallo DNS-achtervoegsel is opgegeven in Hallo */etc/resolv.conf* bestand. De meeste Linux-distributies beheren automatisch Hallo inhoud van dit bestand, dus meestal niet worden bewerkt. U kunt echter Hallo achtervoegsel overschrijven met behulp van Hallo DHCP-client *vervangen* opdracht. toodo dit in */etc/dhcp/dhclient.conf*, toevoegen:

        supersede domain-name <required-dns-suffix>;

