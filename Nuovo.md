```mairmaid

flowchart TD
%% ===============================
%% SWIMLANE PER RUOLI: LOC / DIR / POSTO DI CONTROLLO
%% ===============================

%% ===============================
%% START
START((Start Trasferimento))

%% ===============================
%% LOC
subgraph LOC [LOC]
    A1[Pianifica trasferimento: tipo e quantità]
    A2[Informa DIR della necessità]
    F1[Operai caricano materiale sui muletti]
    F2[Registrazione uscita TRACO in prossimità porta uscita]
    F3[Caricamento materiale nel montacarichi]
    J1[Registrazione materiale TRACO in entrata]
end

%% ===============================
%% DIR
subgraph DIR [DIR]
    B1[Richiede abilitazioni locale partenza e montacarichi]
    D1{Locale destinazione aperto contemporaneamente?}
    E1[Richiede abilitazioni locale destinazione]
    J2[Controfirma registrazione materiale entrato]
    J3[Chiusura porte secondo procedure sicurezza]
end

%% ===============================
%% POSTO DI CONTROLLO
subgraph PC [Posto di Controllo]
    B2{Abilitazioni concesse?}
    E2[Apri porta locale destinazione con chiavi LOC + DIR]
end

%% ===============================
%% FLUSSO
START --> A1 --> A2 --> B1 --> B2
B2 -- NO --> STOP1[Sospensione operazioni] --> END
B2 -- SI --> F1

F1 --> F2 --> F3 --> D1
D1 -- SI --> E1 --> E2 --> F3
D1 -- NO --> F3

F3 --> G1{Altri viaggi necessari?}
G1 -- SI --> F1
G1 -- NO --> J1 --> J2 --> J3 --> END

END((Fine processo))
