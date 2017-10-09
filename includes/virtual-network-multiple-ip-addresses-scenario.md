## <a name="scenario"></a>Scenario
Een virtuele machine met één NIC wordt gemaakt en verbonden tooa virtueel netwerk. Hallo VM vereist drie verschillende *persoonlijke* IP-adressen en de twee *openbare* IP-adressen. Hallo IP-adressen zijn toegewezen toohello IP-configuraties te volgen:

* **IPConfig-1:** wijst een *statische* privé IP-adres en een *statische* openbaar IP-adres.
* **IPConfig-2:** wijst een *statische* privé IP-adres en een *statische* openbaar IP-adres.
* **IPConfig-3:** wijst een *statische* privé IP-adres en er is geen openbare IP-adres.
  
    ![Meerdere IP-adressen](./media/virtual-network-multiple-ip-addresses-scenario/multiple-ipconfigs.png)

Hallo-IP-configuraties zijn gekoppeld toohello NIC wanneer Hallo NIC is gemaakt en Hallo NIC is aangesloten toohello VM wanneer Hallo VM wordt gemaakt. Hallo typen IP-adressen gebruikt voor scenario Hallo dienen ter illustratie. U kunt elk IP-adres en de toewijzing typen dat u nodig hebt.

> [!NOTE]
> Hoewel Hallo stappen in dit artikel alle IP-configuraties tooa wijst één NIC, u kunt ook meerdere IP-configuraties tooany NIC in een VM meerdere NIC's toewijzen. hoe een virtuele machine met meerdere NIC's, toocreate Lees toolearn hello [een virtuele machine maken met meerdere NIC's](../articles/virtual-network/virtual-network-deploy-multinic-arm-ps.md) artikel.
