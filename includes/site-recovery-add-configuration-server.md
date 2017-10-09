1. Hallo Unified Setup-installatiebestand uitvoeren.
2. In **voordat u begint**, selecteer **installeren Hallo configuratieserver en de processerver**.

    ![Voordat u begint](./media/site-recovery-add-configuration-server/combined-wiz1.png)

3. In **van derden softwarelicentie**, klikt u op **ik ga akkoord** toodownload en installeer MySQL.

    ![Software van derden](./media/site-recovery-add-configuration-server/combined-wiz2.png)
4. In **registratie**, selecteer Hallo-registratiesleutel die u hebt gedownload van Hallo kluis.

    ![Registratie](./media/site-recovery-add-configuration-server/combined-wiz3.png)
5. In **internetinstellingen**, hoe Hallo Provider die wordt uitgevoerd op de configuratieserver Hallo tooAzure Site Recovery verbindt via Internet Hallo opgeven.

   a. Als u tooconnect met Hallo-proxy die momenteel ingesteld op de machine hello wilt, selecteer **verbinding maken met Site Recovery via een proxyserver tooAzure**.

   b. Als u rechtstreeks Hallo Provider tooconnect wilt, schakelt **tooAzure siteherstel zonder een proxy-server rechtstreeks verbinding gemaakt**.

   c. Als Hallo bestaande proxy verificatie is vereist als u een aangepaste proxy toouse voor Hallo providerverbinding wilt, schakelt u **verbinding maken met aangepaste proxyinstellingen**.

     * Als u een aangepaste proxy gebruikt, moet u toospecify Hallo adres, poort en referenties.
     * Als u een proxy gebruikt, u moet hebben al toegestaan Hallo URL's die worden beschreven [vereisten](#prerequisites).

     ![Firewall](./media/site-recovery-add-configuration-server/combined-wiz4.png)
6. In **controle van vereisten**, een selectievakje toomake zorgen dat de installatie kunt uitvoeren door Setup wordt uitgevoerd. Als er een waarschuwing wordt weergegeven over Hallo **globale tijd sync selectievakje**, controleren die tijd Hallo op Hallo systeemklok (**datum en tijd** instellingen) is dezelfde als de tijdzone Hallo Hallo.

    ![Vereisten](./media/site-recovery-add-configuration-server/combined-wiz5.png)
7. In **MySQL configuratie**, maken de referenties voor uw aanmelding toohello MySQL server-exemplaar dat is geïnstalleerd.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz6.png)
8. In **omgeving Details**Selecteer of u tooreplicate virtuele VMware-machines gaat. Als u bent, klikt u vervolgens controleert Setup of PowerCLI 6.0 is geïnstalleerd.

    ![MySQL](./media/site-recovery-add-configuration-server/combined-wiz7.png)

9. In **installatielocatie**, selecteer waar u tooinstall Hallo binaire bestanden wilt en Hallo cache opslaan. Hallo station dat u selecteert moet ten minste 5 GB vrije schijfruimte hebben, maar we raden een cachestation met ten minste 600 GB vrije ruimte.

    ![Installatielocatie](./media/site-recovery-add-configuration-server/combined-wiz8.png)
10. In **netwerk selecteren**, Hallo-listener (netwerkadapter en SSL-poort) Geef op welke Hallo configuratie server verzendt en ontvangt gegevens van replicatie. 9443 is Hallo standaardpoort gebruikt voor het verzenden en ontvangen van replicatieverkeer, maar u kunt dit nummer toosuit poort wijzigen vereisten van uw omgeving. Bij toevoeging toohello poort 9443 openen we ook poort 443, die wordt gebruikt door een replicatiebewerkingen web server tooorchestrate. Gebruik geen poort 443 voor het verzenden of ontvangen van replicatieverkeer.

    ![Netwerk selecteren](./media/site-recovery-add-configuration-server/combined-wiz9.png)


11. In **samenvatting**bekijkt hello informatie en op **installeren**. Wanneer de installatie is voltooid, wordt er een wachtwoordzin gegenereerd. U hebt deze nodig bij het inschakelen van de replicatie. Kopieer de wachtwoordzin daarom en bewaar deze op een veilige locatie.

    ![Samenvatting](./media/site-recovery-add-configuration-server/combined-wiz10.png)

Nadat de registratie is voltooid, Hallo-server wordt weergegeven op Hallo **instellingen** > **Servers** blade in Hallo kluis.
