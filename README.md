# High Side Switch

Circuit for high side switch 60V up to 3 kW

# Anforderung

Die Stromversorgung eines Motor-Controllers soll an der High Side (Vss) geschaltet werden. Als Schaltsignal wird die Betriebsspannung (Vss) mit einem geringen Strom im Bereich von maximal einiger Milliampere verwendet. Im Gegensatz zu anderen, sogennanten Anti-Spark-Switches, ist der High Side Switch bei offenem Eingang ausgeschaltet. Daher wird nur ein einziger Schließer benötigt. Die Schaltleitung kann auch an abhängige Signalgeber angeschlossen werden.

# Wieso High Side?

Wird Low Side geschaltet, hängt die Elektronik weiterhin an der Betriebsspannung. Durch mit Masse verbundenen Bauteilen fließt weiter Strom. Dies führt zu unangenehmen Nebeneffekten, permanenten Stromverbrauch etc.

# Hinweise zum Schaltplan

In LTSpice hatte ich nicht exakt die verwendeten Bauteile, derher habe ich ähnliche Beuteile verwendet.

Folgende Bauteile wurden in der Praxis bis 3 kW getestet:

Bauteil | Typ
T1-T4   | SPP80P06PH, Infineon, P-Channel, -60V, -80A, 0,023R
T5      | 2N5551, NPN-Transistor, 160V, 0,6A, 0,63W
D1      | Generische Zener-Diode, 15V, 0,5W
D2      | P6KE56CA, TVS Suppressordiode , 56V, 600W
R[x]    | Widerstand 1/4 Watt
C2      | 220nF, 1ß0V, Polyester (20V reicht auch)

Die restliche Beschaltung ist nur zur Simulation.

# Simulation

1. Bei 1s wird die Versorgungsspannung 54,6V (=Li-Ion 13S) eingeschaltet. Nur ein fast unsichtbarer Spike zu sehen durch Kapazitäten im Picofarad-Bereich.
2. Bei 2s wird die Steuerleitung auf High gelegt. Der Last-Kondensator von 100uF wird geladen. Das verzögerte Ansteigen der Spannung an den Mosfets zieht den Einschaltvorgang einige Millisekunden in die Länge. Dadurch bleibt der Strom unter 50A. Wem das immer noch zu viel ist, kann für C2 auch 1uF nehmen.
3. Bei 3s wird eine Sinusförmige Last zugeschaltet, die abwechselnd bis ca. 1,5kW Leistung zieht und dann wieder leicht rekupperiert.
4. Bei 7s wird die Last abgeschaltet.
5. Bei 8s wird die Steuerleitung hochohmig. Nachdem C2 über 200K entladen wurde, schalten die Mosfets ab.
6. Bei 9s wird die Versorgungsspannung ausgeschaltet.

# Bewertung

Alle Parameter bleiben innerhalb der Spezifikation. Die maximale Leistung an allen 4 Mosfets zusammen beträgt ca. 20 Watt wenn am Verbraucher Leistungsspitzen von 1,5kW angefragt werden. Dazu wurden die 4 Mosfets zusätzlich auf einen kleinen Kühlkörper montiert (siehe Foto).

# Ausblick

Man könnte auch 6 Mosfets des Typs SPP80P06PH verwenden. Bei neuen Projekten mit noch höherer Leistungsaufnahme wird möglicherweise ein High Side Switch mit N-Channel Mosfets realisiert werden. Leider sind entsprechende Bauteile hierzulande inzwischen schwierig zu bekommen.