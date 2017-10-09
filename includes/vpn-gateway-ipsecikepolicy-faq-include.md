### <a name="is-custom-ipsecike-policy-supported-on-all-azure-vpn-gateway-skus"></a>Wordt het aangepaste beleid voor IPsec/IKE op alle Azure VPN Gateway-SKU's ondersteund?
Het aangepaste beleid voor IPsec/IKE wordt ondersteund op Azure VPN-gateways **VpnGw1, VpnGw2, VpnGw3, Standard** en **HighPerformance**. SKU **Basic** wordt NIET ondersteund.

### <a name="how-many-policies-can-i-specify-on-a-connection"></a>Hoeveel beleidsregels kan ik opgeven voor een verbinding?
U kunt maar ***één*** beleidscombinatie opgeven voor een bepaalde verbinding.

### <a name="can-i-specify-a-partial-policy-on-a-connection-eg-only-ike-algorithms-but-not-ipsec"></a>Kan ik een gedeeltelijk beleid opgeven voor een verbinding? (Bijvoorbeeld alleen IKE-algoritmen maar niet IPsec-algoritmen)
Nee, u moet alle algoritmen en parameters opgeven voor zowel IKE (Main Mode) en IPsec (Quick Mode). Gedeeltelijke beleidsspecificatie is niet toegestaan.

### <a name="what-are-hello-algorithms-and-key-strengths-supported-in-hello-custom-policy"></a>Wat zijn Hallo algoritmen en kracht van ondersteund in Hallo aangepast beleid?
Hallo in de volgende tabel geeft een lijst Hallo ondersteund cryptografische algoritmen en kracht kunnen worden geconfigureerd door Hallo-klanten. U moet voor elk veld een optie selecteren.

| **IPsec/IKEv2**  | **Opties**                                                                   |
| ---              | ---                                                                           |
| IKEv2-versleuteling | AES256, AES192, AES128, DES3, DES                                             |
| IKEv2-integriteit  | SHA384, SHA256, SHA1, MD5                                                     |
| DH-groep         | DHGroup24, ECP384, ECP256, DHGroup14 (DHGroup2048), DHGroup2, DHGroup1, geen |
| IPsec-versleuteling | GCMAES256, GCMAES192, GCMAES128, AES256, AES192, AES128, DES3, DES, geen      |
| IPsec-integriteit  | GCMAES256, GCMAES192, GCMAES128, SHA256, SHA1, MD5                            |
| PFS-groep        | PFS24, ECP384, ECP256, PFS2048, PFS2, PFS1, geen                              |
| QM SA-levensduur   | Seconden (geheel getal; **min. 300** /standaard 27000 seconden)<br>KB (geheel getal; **min. 1024**/standaard 102400000 KB)           |
| Verkeersselector | UsePolicyBasedTrafficSelectors ($True/$False; standaard $False)                 |
|                  |                                                                               |

> [!IMPORTANT]
> 1. DHGroup2048 & PFS2048 zijn dezelfde Hallo als Diffie-Hellman-groep **14** in IKE en IPsec PFS. Zie [Diffie-Hellman-groepen](#DH) voor Hallo voltooien toewijzingen.
> 2. GCMAES algoritmen, moet u even GCMAES algoritme en de sleutel lang Hallo voor IPSec-codering en integriteit.
> 3. Levensduur voor de Hoofdmodus IKEv2 wordt vastgesteld op 28.800 seconden op Hallo Azure VPN-gateways
> 4. De QM SA-levensduur is een optionele parameter. Als niets is opgegeven, worden de standaardwaarden 27.000 seconden (7,5 uur) en 102400000 KB (102 GB) gebruikt.
> 5. UsePolicyBasedTrafficSelector is een parameter optie op Hallo-verbinding. Raadpleeg de volgende veelgestelde vragen over Hallo-item voor 'UsePolicyBasedTrafficSelectors'

### <a name="does-everything-need-toomatch-between-hello-azure-vpn-gateway-policy-and-my-on-premises-vpn-device-configurations"></a>Heeft alles toomatch tussen hello Azure VPN-gateway beleid en Mijn lokale VPN-apparaatconfiguraties nodig?
De configuratie van uw lokale VPN-apparaat moet overeenkomen met of bevatten Hallo volgende algoritmen en parameters die u opgeeft op Hallo Azure IPsec/IKE-beleid:

* IKE-versleutelingsalgoritme
* IKE-integriteitsalgoritme
* DH-groep
* IPsec-versleutelingsalgoritme
* IPsec-integriteitsalgoritme
* PFS-groep
* Verkeersselector (*)

Hallo SA levensduur zijn alleen lokale specificaties, toomatch niet nodig.

Als u inschakelt **UsePolicyBasedTrafficSelectors**, moet u uw VPN-apparaat heeft een overeenkomende verkeer selectoren gedefinieerd met behulp van alle combinaties van uw lokale netwerk (lokale netwerkgateway) voorvoegsels van Hallo Hallo tooensure Virtuele Azure-netwerkvoorvoegsels in plaats van any-to-any. Als uw lokale netwerkvoorvoegsels 10.1.0.0/16 en 10.2.0.0/16 zijn, en de voorvoegsels van uw virtuele netwerk 192.168.0.0/16 en 172.16.0.0/16 zijn, moet u bijvoorbeeld toospecify Hallo verkeer selectoren te volgen:
* 10.1.0.0/16 <====> 192.168.0.0/16
* 10.1.0.0/16 <====> 172.16.0.0/16
* 10.2.0.0/16 <====> 192.168.0.0/16
* 10.2.0.0/16 <====> 172.16.0.0/16

Raadpleeg te[verbinding maken met meerdere on-premises op beleid gebaseerde VPN-apparaten](../articles/vpn-gateway/vpn-gateway-connect-multiple-policybased-rm-ps.md) voor meer informatie over het toouse deze optie.

### <a name ="DH"></a>Welke Diffie-Hellman-groepen worden ondersteund?
Hallo in de volgende tabel geeft een overzicht van Hallo ondersteund Diffie-Hellman-groepen voor IKE (DHGroup) en IPsec (PFSGroup):

| **Diffie-Hellman-groep**  | **DHGroup**              | **PFSGroup** | **Sleutellengte** |
| ---                       | ---                      | ---          | ---            |
| 1                         | DHGroup1                 | PFS1         | 768-bits MODP   |
| 2                         | DHGroup2                 | PFS2         | 1024-bits MODP  |
| 14                        | DHGroup14<br>DHGroup2048 | PFS2048      | 2048-bits MODP  |
| 19                        | ECP256                   | ECP256       | 256-bits ECP    |
| 20                        | ECP384                   | ECP284       | 384-bits ECP    |
| 24                        | DHGroup24                | PFS24        | 2048-bits MODP  |
|                           |                          |              |                |

Raadpleeg te[RFC3526](https://tools.ietf.org/html/rfc3526) en [RFC5114](https://tools.ietf.org/html/rfc5114) voor meer informatie.

### <a name="does-hello-custom-policy-replace-hello-default-ipsecike-policy-sets-for-azure-vpn-gateways"></a>Vervangt het aangepaste beleid Hallo Hallo standaard IPsec/IKE-beleid sets voor Azure VPN-gateways?
Ja, als een aangepast beleid op een verbinding is opgegeven, Azure VPN-gateway alleen beleid wordt gebruikt Hallo Hallo verbinding, zowel als IKE initiator als responder IKE.

### <a name="if-i-remove-a-custom-ipsecike-policy-does-hello-connection-become-unprotected"></a>Als ik een aangepast beleid voor IPsec/IKE verwijdert, Hallo verbinding treedt onbeveiligde?
Nee, Hallo verbinding nog steeds worden beveiligd met IPsec/IKE. Wanneer u een aangepast beleid Hallo van een verbinding verwijdert, hello Azure VPN-gateway wordt de gegevensmodelversie teruggezet back toohello [standaardlijst met IPsec/IKE voorstellen](../articles/vpn-gateway/vpn-gateway-about-vpn-devices.md) en opnieuw starten Hallo IKE-handshake opnieuw met uw on-premises VPN-apparaat.

### <a name="would-adding-or-updating-an-ipsecike-policy-disrupt-my-vpn-connection"></a>Kan het toevoegen of bijwerken van een beleid voor IPsec/IKE mijn VPN-verbinding verstoren?
Ja, leidt tot een onderbreking van de kleine (een paar seconden) zoals hello Azure VPN-gateway wordt moeten Hallo bestaande verbinding verbreken en opnieuw Hallo IKE-handshake toore starten-Hallo IPSec-tunnel met Hallo nieuwe cryptografische algoritmen en parameters maakt. Zorg ervoor dat uw on-premises VPN-apparaat wordt ook geconfigureerd met overeenkomende Hallo-algoritmen en kracht van toominimize hello wordt onderbroken.

### <a name="can-i-use-different-policies-on-different-connections"></a>Kan ik verschillende beleidsregels voor verschillende verbindingen gebruiken?
Ja. Aangepast beleid wordt per verbinding toegepast. U kunt verschillende IPsec/IKE-beleidsregels toepassen op verschillende verbindingen. U kunt aangepaste beleidsregels op een subset van verbindingen ook tooapply. Hallo resterende toepassingsgroepen hello Azure standaard IPsec/IKE-beleid wordt gebruikt.

### <a name="can-i-use-hello-custom-policy-on-vnet-to-vnet-connection-as-well"></a>Kan ik Hallo aangepast beleid op en VNet-naar-VNet-verbinding gebruiken?
Ja, u kunt een aangepast beleid toepassen op zowel cross-premises IPsec-verbindingen als VNet-naar-VNet-verbindingen.

### <a name="do-i-need-toospecify-hello-same-policy-on-both-vnet-to-vnet-connection-resources"></a>Moet ik toospecify Hallo hetzelfde beleid op beide resources VNet-naar-VNet-verbinding?
Ja. Een VNet-naar-VNet-tunnel bestaat uit twee verbindingsresources in Azure, één voor elke richting. U moet tooensure beide resources verbinding hebben hetzelfde beleid Hallo othereise hello VNet-naar-VNet-verbinding niet tot stand brengen.

### <a name="does-custom-ipsecike-policy-work-on-expressroute-connection"></a>Werkt een aangepast IPsec/IKE-beleid op een ExpressRoute-verbinding?
Nee. IPsec/IKE-beleid werkt alleen op S2S VPN- en VNet-naar-VNet-verbindingen via hello Azure VPN-gateways.
