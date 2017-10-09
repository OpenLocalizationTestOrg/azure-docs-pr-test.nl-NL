In deze stap maakt u een regel tooopen Hallo test firewallpoort voor Hallo taakverdeling eindpunt (zoals eerder opgegeven 59999) en een andere regel tooopen Hallo poort beschikbaarheidsgroeplistener. Omdat u Netwerktaakverdeling Hallo-eindpunt op Hallo virtuele machines die replica's van beschikbaarheidsgroepen bevatten gemaakt, moet u tooopen Hallo testpoort en Hallo-listener-poort op Hallo respectieve virtuele machines.

1. Start op virtuele machines die als host fungeren van replica's, **Windows Firewall met geavanceerde beveiliging**.

2. Met de rechtermuisknop op **regels voor binnenkomende verbindingen**, en klik vervolgens op **nieuwe regel**.

3. Op Hallo **regeltype** pagina **poort**, en klik vervolgens op **volgende**.

4. Op Hallo **protocollen en poorten** pagina **TCP**, type **59999** in Hallo **specifieke lokale poorten** vak en klik vervolgens op **Volgende**.

5. Op Hallo **actie** pagina, houden **Hallo verbinding toestaan** geselecteerd en klik vervolgens op **volgende**.

6. Op Hallo **profiel** pagina, Hallo standaardinstellingen accepteren en klik vervolgens op **volgende**.

7. Op Hallo **naam** pagina in Hallo **naam** tekst, geeft u de regelnaam van een, zoals **altijd op Listener-test poort**, en klik vervolgens op **voltooien**.

8. Herhaal Hallo voorgaande stappen voor het Hallo poort beschikbaarheidsgroeplistener (zoals opgegeven eerder in Hallo $EndpointPort-parameter van het script Hallo) en geef vervolgens een naam voor de desbetreffende regel, zoals **altijd op Listener-poort**.

