# Rischio.mqh

Libreria MQL5 per il calcolo automatico del lottaggio in base alla gestione del rischio.

## Funzionalità

- Calcolo lotti tramite rischio fisso in denaro
- Calcolo lotti tramite rischio percentuale del saldo
- Compounding automatico
- Calcolo lotti tramite Kelly Criterion
- Compatibile con qualsiasi simbolo supportato da MetaTrader 5

---

## Installazione

Copia il file:

```
Rischio.mqh
```

nella cartella:

```
MQL5\Include\
```

e includilo nel tuo Expert Advisor:

```cpp
#include <Rischio.mqh>
```

---

## Creazione dell'oggetto

```cpp
CRischio rischio;
```

---

# Metodi Disponibili

## Compounding()

Calcola automaticamente il nuovo lottaggio in base alla crescita del saldo.

### Parametri

| Parametro | Tipo | Descrizione |
|------------|------|-------------|
| Lotti_Iniziali | double | Lottaggio iniziale |

### Esempio

```cpp
CRischio rischio;

double lots = rischio.Compounding(0.10);

Print("Lotti: ", lots);
```

---

## RischioinDenaro()

Calcola il lottaggio rischiando una quantità fissa di denaro.

### Parametri

| Parametro | Tipo | Descrizione |
|------------|------|-------------|
| denaro | double | Importo da rischiare |
| range_stop | double | Distanza dello stop loss |

### Esempio

```cpp
CRischio rischio;

double lots = rischio.RischioinDenaro(100, 500);

Print("Lotti: ", lots);
```

---

## RischioinPercentuale()

Calcola il lottaggio rischiando una percentuale del saldo.

### Parametri

| Parametro | Tipo | Descrizione |
|------------|------|-------------|
| percentuale | double | Percentuale da rischiare |
| range_stop | double | Distanza dello stop loss |

### Esempio

```cpp
CRischio rischio;

double lots = rischio.RischioinPercentuale(1, 500);

Print("Lotti: ", lots);
```

---

## CalcoloLottiKellyFormula()

Calcola il lottaggio utilizzando il Kelly Criterion.

### Parametri

| Parametro | Tipo | Descrizione |
|------------|------|-------------|
| Probablita_Successo | double | Win Rate (%) |
| Rischio_Rendimento | double | Rapporto Risk Reward |
| grandezza_stop | double | Stop Loss |

### Esempio

```cpp
CRischio rischio;

double lots = rischio.CalcoloLottiKellyFormula(
   55,   // Win Rate
   2.0,  // RR
   500   // Stop
);

Print("Lotti Kelly: ", lots);
```

---

# Esempio Completo

```cpp
#include <Rischio.mqh>

CRischio rischio;

void OnTick()
{
   double lots = rischio.RischioinPercentuale(1.0, 500);

   Print("Lottaggio calcolato: ", lots);
}
```

---

# Note

- `range_stop` deve essere espresso nella stessa unità utilizzata dal broker.
- La libreria utilizza:
  - `SYMBOL_TRADE_TICK_SIZE`
  - `SYMBOL_TRADE_TICK_VALUE_LOSS`
  - `SYMBOL_VOLUME_STEP`
- In caso di dati non validi viene restituito `0`.

---

# Licenza

MIT License
