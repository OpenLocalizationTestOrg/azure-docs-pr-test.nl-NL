---
title: aaaSecure een cluster met Windows met behulp van Windows-beveiliging | Microsoft Docs
description: Meer informatie over hoe tooconfigure knooppunt naar clientknooppunt beveiliging en op een zelfstandige cluster dat wordt uitgevoerd in Windows met behulp van Windows-beveiliging.
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: ce3bf686-ffc4-452f-b15a-3c812aa9e672
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: dekapur
ms.openlocfilehash: 44f3011eb630357f342052a48d6c852b17dccec4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: nl-NL
ms.lasthandoff: 10/06/2017
---
# <a name="secure-a-standalone-cluster-on-windows-by-using-windows-security"></a>Een zelfstandige cluster op Windows beveiligen met behulp van Windows-beveiliging
tooprevent onbevoegde toegang tooa Service Fabric-cluster, moet u Hallo-cluster beveiligen. Beveiliging is vooral belangrijk bij Hallo cluster productieworkloads wordt uitgevoerd. Dit artikel wordt beschreven hoe tooconfigure knooppunt naar beveiliging en op client-naar-knooppunt met behulp van Windows-beveiliging in Hallo *ClusterConfig.JSON* bestand.  Hallo proces toohello overeenkomt met configureren van beveiligingsstap van [maken van een zelfstandige cluster waarop Windows](service-fabric-cluster-creation-for-windows-server.md). Zie voor meer informatie over hoe Service Fabric Windows-beveiliging gebruikt [security scenario's](service-fabric-cluster-security.md).

> [!NOTE]
> U moet zorgvuldig Hallo selectie van knooppunt naar beveiliging omdat er geen cluster-upgrade van één beveiliging keuze tooanother. toochange Hallo beveiliging selectie, hebt u volledige toorebuild Hallo-cluster.
>
>

## <a name="configure-windows-security-using-gmsa"></a>Windows-beveiliging met behulp van gMSA configureren  
Hallo voorbeeld *ClusterConfig.gMSA.Windows.MultiMachine.JSON* configuratiebestand is gedownload met Hallo [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) zelfstandige clusterpakket bevat een sjabloon voor het configureren van Windows-beveiliging gebruikt [groep beheerde serviceaccounts (gMSA)](https://technet.microsoft.com/library/hh831782.aspx):  

```  
"security": {  
            "WindowsIdentities": {  
                "ClustergMSAIdentity": "accountname@fqdn"  
                "ClusterSPN": "fqdn"  
                "ClientIdentities": [  
                    {  
                        "Identity": "domain\\username",  
                        "IsAdmin": true  
                    }  
                ]  
            }  
        }  
```  
  
| **Configuratie-instelling** | **Beschrijving** |  
| --- | --- |  
| WindowsIdentities |Hallo-cluster en de client identiteiten bevat. |  
| ClustergMSAIdentity |Hiermee configureert u een knooppunt naar beveiliging. Een groep beheerd serviceaccount. |  
| ClusterSPN |FQDN-SPN voor de gMSA-account|  
| ClientIdentities |Hiermee configureert u clientknooppunt beveiliging. Een matrix van gebruikersaccounts van de client. |  
| Identiteit |Hallo identiteit van de client, een domeingebruiker. |  
| IsAdmin |Waar geeft dat die Hallo domein de gebruiker heeft beheerderstoegang client, false voor clienttoegang van de gebruiker. |  
  
[Knooppunt toonode beveiliging](service-fabric-cluster-security.md#node-to-node-security) is geconfigureerd door in te stellen **ClustergMSAIdentity** wanneer het service fabric moet toorun onder gMSA. In de volgorde toobuild vertrouwensrelaties tussen knooppunten, moeten ze worden aangebracht op de hoogte van elkaar. Dit op twee verschillende manieren kunt worden bereikt: Hallo groep beheerd serviceaccount gebruiken met alle knooppunten in cluster Hallo opgeven, of Hallo machine domeingroep die alle knooppunten in het Hallo-cluster omvat. Ten zeerste aangeraden Hallo [groep beheerde serviceaccounts (gMSA)](https://technet.microsoft.com/library/hh831782.aspx) benadering, met name voor grotere clusters (meer dan 10 knooppunten) of voor clusters die zijn waarschijnlijk toogrow of te verkleinen.  
Deze aanpak is niet vereist voor Hallo maken van een domeingroep waarvoor clusterbeheerders toegang rechten tooadd hebben gekregen en verwijder leden. Deze accounts zijn ook nuttig voor het automatisch wachtwoordbeheer. Zie voor meer informatie [aan de slag met beheerde serviceaccounts voor groepen](http://technet.microsoft.com/library/jj128431.aspx).  
 
[De clientbeveiligingssessie toonode](service-fabric-cluster-security.md#client-to-node-security) is geconfigureerd met **ClientIdentities**. In de volgorde tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow configureren welke client-id's die kunnen worden vertrouwd. Dit kan op twee verschillende manieren worden gedaan: Geef Hallo groep Domeingebruikers die kunnen verbinding maken of geef Hallo knooppunt domeingebruikers die verbinding kunnen maken. Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn: beheerder en gebruiker. Toegangsbeheer biedt Hallo mogelijkheid voor Hallo beheerder toolimit toegang toocertain clustertypen van bewerkingen voor verschillende groepen gebruikers, Hallo cluster veiliger maken voor een cluster.  Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services. Zie voor meer informatie over toegangsbeheer [toegangsbeheer voor Service Fabric-clients op basis van rollen](service-fabric-cluster-security-roles.md).  
 
Hallo volgende voorbeeld **beveiliging** sectie configureert u Windows-beveiliging met behulp van gMSA en geeft aan dat Hallo machines in *ServiceFabric.clusterA.contoso.com* gMSA maken deel uit van het Hallo-cluster en die *CONTOSO\usera* admin clienttoegang heeft:  
  
```  
"security": {  
    "WindowsIdentities": {  
        "ClustergMSAIdentity" : "ServiceFabric.clusterA.contoso.com",  
        "ClusterSPN" : "clusterA.contoso.com",  
        "ClientIdentities": [{  
            "Identity": "CONTOSO\\usera",  
            "IsAdmin": true  
        }]  
    }  
}  
```  
  
## <a name="configure-windows-security-using-a-machine-group"></a>Windows-beveiliging met behulp van een machine-beheergroep configureren  
Hallo voorbeeld *ClusterConfig.Windows.MultiMachine.JSON* configuratiebestand is gedownload met Hallo [Microsoft.Azure.ServiceFabric.WindowsServer.<version>. ZIP](http://go.microsoft.com/fwlink/?LinkId=730690) zelfstandige clusterpakket bevat een sjabloon voor het configureren van Windows-beveiliging.  Windows-beveiliging is geconfigureerd in Hallo **eigenschappen** sectie: 

```
"security": {
            "ClusterCredentialType": "Windows",
            "ServerCredentialType": "Windows",
            "WindowsIdentities": {
                "ClusterIdentity" : "[domain\machinegroup]",
                "ClientIdentities": [{
                    "Identity": "[domain\username]",
                    "IsAdmin": true
                }]
            }
        }
```

| **Configuratie-instelling** | **Beschrijving** |
| --- | --- |
| ClusterCredentialType |**ClusterCredentialType** te is ingesteld,*Windows* als ClusterIdentity is opgegeven voor een Active Directory-groep computernaam. |  
| ServerCredentialType |Stel te*Windows* tooenable Windows-beveiliging voor clients.<br /><br />Dit betekent dat clients Hallo van Hallo en Hallo cluster zichzelf worden uitgevoerd binnen een Active Directory-domein. |  
| WindowsIdentities |Hallo-cluster en de client identiteiten bevat. |  
| ClusterIdentity |Gebruik een machine groepsnaam, domain\machinegroup, tooconfigure knooppunt naar beveiliging. |  
| ClientIdentities |Hiermee configureert u clientknooppunt beveiliging. Een matrix van gebruikersaccounts van de client. |  
| Identiteit |Hallo domeingebruiker, domein\gebruikersnaam voor de identiteit van de client Hallo toevoegen. |  
| IsAdmin |Set tootrue toospecify die Hallo domeingebruiker heeft clienttoegang als beheerder of ONWAAR voor clienttoegang van de gebruiker. |  

[Knooppunt toonode beveiliging](service-fabric-cluster-security.md#node-to-node-security) is geconfigureerd met behulp van instelling **ClusterIdentity** als u wilt dat toouse een Machinegroep binnen een Active Directory-domein. Zie voor meer informatie [maken van een Machine-groep in Active Directory](https://msdn.microsoft.com/library/aa545347(v=cs.70).aspx).

[Beveiliging van de client naar het knooppunt](service-fabric-cluster-security.md#client-to-node-security) is geconfigureerd met behulp van **ClientIdentities**. tooestablish vertrouwensrelatie tussen een client en het Hallo-cluster, moet u Hallo cluster tooknow Hallo client, identiteiten die Hallo cluster vertrouwen kunnen configureren. U kunt een vertrouwensrelatie in twee verschillende manieren:

- Geef Hallo groep Domeingebruikers die verbinding kunnen maken.
- Geef Hallo knooppunt domeingebruikers die verbinding kunnen maken.

Service Fabric ondersteunt twee verschillende toegangsrechten besturingselementtypen voor clients die verbonden tooa Service Fabric-cluster zijn: beheerder en gebruiker. Toegangsbeheer kan Hallo beheerder toolimit toegang toocertain clustertypen van clusterbewerkingen voor verschillende groepen gebruikers, waardoor Hallo cluster beter te beveiligen.  Beheerders hebben volledige toegang toomanagement mogelijkheden (inclusief lezen/schrijven-mogelijkheden). Gebruikers hebben standaard alleen leestoegang toomanagement mogelijkheden (bijvoorbeeld querymogelijkheden) en Hallo mogelijkheid tooresolve toepassingen en services.  

Hallo volgende voorbeeld **beveiliging** sectie Windows-beveiliging configureert, geeft aan dat Hallo machines in *ServiceFabric/clusterA.contoso.com* deel uitmaken van Hallo-cluster en geeft aan dat  *CONTOSO\usera* admin clienttoegang heeft:

```
"security": {
    "ClusterCredentialType": "Windows",
    "ServerCredentialType": "Windows",
    "WindowsIdentities": {
        "ClusterIdentity" : "ServiceFabric/clusterA.contoso.com",
        "ClientIdentities": [{
            "Identity": "CONTOSO\\usera",
            "IsAdmin": true
        }]
    }
},
```

> [!NOTE]
> Service Fabric moeten niet worden geïmplementeerd op een domeincontroller. Zorg ervoor dat ClusterConfig.json niet Hallo IP-adres van de domeincontroller Hallo opnemen wanneer u een Machinegroep of groep beheerde serviceaccounts (gMSA).
>
>

## <a name="next-steps"></a>Volgende stappen
Na het configureren van Windows-beveiliging in Hallo *ClusterConfig.JSON* bestand, hervat Hallo cluster maakproces in [maken van een zelfstandige cluster waarop Windows](service-fabric-cluster-creation-for-windows-server.md).

Voor meer informatie over hoe naar knooppunten beveiliging, client-naar-node beveiliging en op rollen gebaseerde toegangsbeheer, Zie [security scenario's](service-fabric-cluster-security.md).

Zie [Connect tooa beveiligde cluster](service-fabric-connect-to-secure-cluster.md) voor voorbeelden van verbinding maken met behulp van PowerShell of FabricClient.
