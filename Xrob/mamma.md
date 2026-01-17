```mermaid

flowchart TD
%% Roles are implicit based on the image

START[BAN invia mail dettaglio lotti in consegna] --> PREDISPONE[BAN predispone lista personale che consegna]

PREDISPONE --> AUTORIZZA[BAN autorizza lista 1° livello]
AUTORIZZA --> ABILITA[BAN abilita montacarichi - 5,57]
AUTORIZZA --> APPROVA[LOC approva lista 1° livello]
APPROVA --> DIR_ABILITA[DIR abilita montacarichi +3,20]

ABILITA --> CARICA[BAN carica montacarichi 1 lotto]
DIR_ABILITA --> CARICA

CARICA --> VERIFICA[LOC + DIR verificano lotto]

VERIFICA --> IMPERFEZIONI{Lotto con imperfezioni?}
IMPERFEZIONI -- SI --> SEGNALATO[Lotto segnalato per lavorazione speciale]
IMPERFEZIONI -- NO --> REGOLARE[Lotto regolare]

SEGNALATO --> IN_SACRISTIA[Lotto in sacristia registrato da DIR + LOC]
REGOLARE --> IN_SACRISTIA

IN_SACRISTIA --> FIRMA[Firma mod. St. cassa da BAN-DIR-LOC]

IN_SACRISTIA --> CONSEGNA{Consegna lotti terminata?}
CONSEGNA -- NO --> CARICA
CONSEGNA -- SI --> END[FINE]

