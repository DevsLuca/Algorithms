```mermaid

flowchart TD
%% Diagramma operativo: Trasferimento materiale

START[LOC predispone trasferimento] --> RICHIEDI_ABILITAZIONE[DIR chiede abilitazione montacarichi e apertura locale origine al PDC]

RICHIEDI_ABILITAZIONE --> APERTURA_ORIGINE[DIR + LOC aprono sacristia origine]

APERTURA_ORIGINE --> POSSIBILE_DESTINAZIONE{È possibile aprire contemporaneamente sacristia destinazione?}
POSSIBILE_DESTINAZIONE -- SI --> RICHIEDI_DESTINAZIONE[DIR chiede abilitazione sacristia destinazione al PDC]
RICHIEDI_DESTINAZIONE --> APERTURA_DESTINAZIONE[DIR + LOC aprono sacristia destinazione]

POSSIBILE_DESTINAZIONE -- NO --> CARICO_ORIGINE[In sacristia origine viene caricato materiale sui muletti]

APERTURA_DESTINAZIONE --> CARICO_ORIGINE

CARICO_ORIGINE --> REGISTRAZIONE[DIR + LOC registrano materiale in uscita]

REGISTRAZIONE --> CARICO_MONTACARICHI[Materiale caricato su montacarichi]

CARICO_MONTACARICHI --> MONTACARICHI_PIENO{Montacarichi pieno?}
MONTACARICHI_PIENO -- NO --> CARICO_MONTACARICHI
MONTACARICHI_PIENO -- SI --> CHIAMATA[Chiama montacarichi al piano destinazione]

CHIAMATA --> SCARICO[Operai scaricano montacarichi]

SCARICO --> SAC_DESTINAZIONE_APERTA{Sacristia destinazione aperta?}
SAC_DESTINAZIONE_APERTA -- NO --> LOOP_CARICO[Operai sistemano materiale in sacristia destinazione] --> CARICO_MONTACARICHI
SAC_DESTINAZIONE_APERTA -- SI --> FINE_TRASFERIMENTO{Trasferimento terminato?}
FINE_TRASFERIMENTO -- NO --> CARICO_MONTACARICHI
FINE_TRASFERIMENTO -- SI --> END[FINE PROCESSO]



