# Progettazione e Modellizzazione di un Sensore di Vibrazione Piezoelettrico: Il Caso del Pickup per Grammofono

[cite_start]La progettazione di un sensore piezoelettrico richiede la comprensione dell'accoppiamento bidirezionale tra il dominio meccanico e quello elettrico[cite: 71]. Di seguito viene analizzata la fisica fondamentale del fenomeno, per poi applicarla alla modellizzazione e all'analisi dinamica di un caso applicativo specifico: un pickup (fonorivelatore) per grammofono basato su una lamina di Titanato Zirconato di Piombo (PZT) sollecitata da un braccio metallico dotato di punta di lettura.

---

## 1. Il Fenomeno Fisico e le Equazioni Costitutive

[cite_start]La piezoelettricità è una proprietà lineare di alcune classi di materiali cristallini privi di centro di simmetria, scoperta nel 1880-81 dai fratelli Curie[cite: 4, 12]. Essa si manifesta attraverso due modalità principali:
* [cite_start]**Effetto diretto (Rilevazione):** Una sollecitazione o sforzo meccanico ($T$) induce una separazione di carica elettrica, espressa in termini di spostamento o induzione dielettrica ($D$)[cite: 6, 75, 76]. [cite_start]Questo effetto viene sfruttato nella realizzazione di sensori[cite: 9, 319].
* [cite_start]**Effetto inverso o converso (Generazione):** L'applicazione di un campo elettrico ($E$) sviluppa una deformazione meccanica o strain ($S$)[cite: 7, 74, 77]. [cite_start]Questo effetto viene invece sfruttato negli attuatori[cite: 11, 22, 317].

[cite_start]Nel caso delle ceramiche policristalline ferroelettriche come il PZT, i dipoli elettrici sono originariamente organizzati in domini orientati in modo casuale[cite: 53, 55, 56, 58]. [cite_start]Al di sopra della temperatura di Curie ($T_{\text{Curie}}$), i domini perdono l'orientamento e il materiale smette di esibire proprietà piezoelettriche[cite: 58]. [cite_start]Per rendere attiva la ceramica, essa subisce un processo di **poling** (polarizzazione), in cui l'applicazione di un forte campo elettrico orienta permanentemente i domini lungo un asse specifico [cite: 63, 64][cite_start], convenzionalmente denominato asse 3 (asse di polarizzazione)[cite: 136].



[cite_start]Per una trattazione monodimensionale semplificata, l'interazione tra il dominio elettrico e meccanico è descritta dalle seguenti **equazioni costitutive lineari** (espresse nella forma che assume come variabili indipendenti lo sforzo $T$ e il campo elettrico $E$)[cite: 71, 72, 130]:

$$\begin{cases} 
S = s^{E}T + dE \\ 
D = dT + \epsilon^{T}E 
\end{cases}$$

Dove:
* [cite_start]$S$ è la deformazione meccanica o strain ($\text{m/m}$)[cite: 74].
* [cite_start]$T$ è lo sforzo meccanico o stress ($\text{N/m}^2$)[cite: 75].
* [cite_start]$E$ è il campo elettrico ($\text{V/m}$)[cite: 77, 78].
* [cite_start]$D$ è lo spostamento dielettrico o densità di carica superficiale ($\text{C/m}^2$)[cite: 76].
* [cite_start]$s^{E}$ è la cedevolezza elastica (compliance) del materiale valutata a campo elettrico costante (ossia in condizioni di cortocircuito elettrico, $E=0$) ($\text{m}^2/\text{N}$)[cite: 79, 80].
* [cite_start]$\epsilon^{T}$ è la permittività dielettrica valutata a sforzo costante (ossia con materiale meccanicamente libero di deformarsi, $T=0$) ($\text{F/m}$)[cite: 83, 84].
* [cite_start]$d$ è il **coefficiente piezoelettrico di carica** ($\text{C/N}$ oppure $\text{m/V}$)[cite: 73, 85].

[cite_start]Nel caso di un sensore di vibrazione (che sfrutta l'effetto diretto), il termine fondamentale è proprio il coefficiente $d$, il quale esprime la proporzionalità diretta tra lo sforzo applicato e la densità di carica generata[cite: 156, 157].

---

## 2. Il Sistema Fisico: Pickup per Grammofono

Si consideri l'applicazione in cui l'elemento piezoelettrico funge da pickup (fonorivelatore) per la riproduzione audio analogica. Il sistema è schematicamente composto da:
1. Una **punta di lettura** (es. diamante o zaffiro) che segue geometricamente le microscopiche ondulazioni incise sulle pareti del solco del disco in vinile.
2. Un **braccio metallico rigido** (cantilever) che funge da trasmissione meccanica, trasferendo lo spostamento della punta verso il trasduttore piezoelettrico.
3. Un elemento sensibile in ceramica **PZT-5H** vincolato all'interno del corpo del pickup.

[Ancoraggio Fisso del Pickup]
                          |
                    +-----+-----+
                    |  Elemento |  <-- Elettrodi (Uscita V)
                    |   PZT-5H  |
                    +-----+-----+
                          | (Sollecitazione Meccanica)
===========================+ [Pivot / Snodo]
^ Braccio Metallico (Cantilever)
|
[Punta]
|

### Scelta del Materiale e Direzioni di Taglio (La Matrice $d_{ij}$)
I materiali piezoelettrici sono mezzi tridimensionali anisotropi[cite: 92]. Le loro proprietà dipendono fortemente dalla direzione della sollecitazione rispetto all'asse di polarizzazione indotto dal poling[cite: 128, 136]. Per questa ragione, i coefficienti vengono descritti tramite notazione a indici ridotti $d_{ij}$ [cite: 103, 132]: il primo indice ($i$) indica la direzione dell'asse elettrico (direzione del campo o della carica), mentre il secondo indice ($j$) indica la direzione della sollecitazione meccanica[cite: 157].

Esaminando le proprietà dei materiali disponibili nella scheda tecnica[cite: 158]:
* Il **Quarzo** (monocristallo) offre un coefficiente stazionario ma ridotto ($d_{11} = 2.3 \text{ pC/N}$)[cite: 53, 158].
* Il **PZT-5H** (ceramica ferroelettrica) esibisce risposte accoppiate eccezionalmente elevate: un coefficiente longitudinale $d_{33} = 593 \text{ pC/N}$ e un coefficiente trasversale $d_{31} = -274 \text{ pC/N}$[cite: 53, 158].

Nel braccio meccanico del grammofono, la vibrazione geometrica impressa dal solco $x(t)$ induce uno spostamento dinamico della punta. Il braccio metallico trasferisce questo movimento applicando una forza sull'elemento in PZT. A seconda del montaggio, si può configurare il sistema per lavorare in:
* **Compressione/Trazione (Modo $d_{31}$ o $d_{33}$):** La vibrazione induce flessione nella lamina di PZT, generando sforzi normali che si traducono in una tensione elettrica raccolta sugli elettrodi disposti lungo l'asse 3[cite: 136, 143, 144].
* **Taglio (Modo $d_{15}$):** Sfruttando il coefficiente di taglio molto elevato del PZT-5H ($d_{15} = 741 \text{ pC/N}$) [cite: 158], il movimento laterale del braccio metallico applica una sollecitazione di taglio rispetto all'asse di polarizzazione, massimizzando il segnale elettrico d'uscita a parità di forza meccanica impresso dal solco[cite: 134, 135].

---

## 3. Modellizzazione Circuitale Equivalente

Per analizzare il comportamento del pickup a frequenze inferiori rispetto alla prima risonanza meccanica strutturale, è possibile convertire le relazioni costitutive locali in variabili elettromeccaniche globali: Forza ($F$), Spostamento ($X$), Tensione ($V$) e Corrente ($I$)[cite: 250, 252]. 

Integrando sulla geometria della lamina di PZT (definendo l'area degli elettrodi come $A$ e lo spessore dell'elemento come $l$), si ottiene il circuito equivalente elettromeccanico basato su un **trasformatore ideale operante anche in DC**[cite: 255, 267]:



Le equazioni alle porte del sistema, considerando il fattore di trasformazione ideale $\alpha = \frac{eA}{l}$ (dove $e$ è il coefficiente piezoelettrico di sforzo) [cite: 73, 263], sono espresse da[cite: 255]:

$$\begin{cases} 
F = k^{E}X - \alpha V \\ 
I = \alpha j\omega X + j\omega C^{S}V 
\end{cases}$$

Esaminando il solo dominio elettrico d'uscita (lato secondario del trasformatore), l'effetto diretto della vibrazione meccanica converte la forza applicata dal braccio in una separazione di carica. Integrando la corrente nel tempo ($Q = \int I dt$), il pickup piezoelettrico è modellizzato a basse frequenze come un **generatore di carica $Q$ proporzionale alla forza, posto in parallelo alla propria capacità elettrica libera $C^{T}$**[cite: 252, 297]:

$$Q = d_{ij} \cdot F_{\text{meccanica}}(t)$$

La capacità propria del sensore in condizioni meccanicamente libere (ovvero libero di flettersi sotto l'azione del braccio, senza vincoli rigidi esterni) è definita come[cite: 297]:
$$C^{T} = C^{S} + \frac{A}{l}ed$$

---

## 4. Analisi dei Vincoli ed Effetti Elettromeccanici sul Braccio di Lettura

L'interazione tra il braccio metallico del grammofono e l'interfaccia elettrica del pickup introduce fenomeni fisici che influenzano direttamente la fedeltà della riproduzione audio:

### Modificazione della Costante Elastica ($k^{E}$ vs $k^{D}$)
La rigidezza meccanica che la punta del grammofono incontra muovendosi nel solco non è costante, ma è strettamente legata alle condizioni al contorno elettriche applicate agli elettrodi del PZT[cite: 279, 280]:
* **Condizione di Circuito Aperto:** Se il pickup è collegato a uno stadio di lettura ad altissima impedenza (nessun flusso di corrente, $I=0$), le cariche accumulate sugli elettrodi non possono muoversi[cite: 294]. Questo accumulo genera un campo elettrico interno che si oppone alla deformazione meccanica, facendo apparire il materiale **più rigido**[cite: 296]. La costante elastica del sistema sale al valore $k^{D}$[cite: 296]:
  $$k^{D} = k^{E} + \frac{A}{l}eh > k^{E}$$
* **Condizione di Cortocircuito Virtuale:** Se il pickup è interfacciato a un amplificatore a bassa impedenza d'ingresso (es. amplificatore di carica), le cariche fluiscono liberamente annullando il campo elettrico interno[cite: 282]. In questo caso la rigidezza meccanica scende al suo valore minimo $k^{E}$[cite: 283].

L'efficienza di questa interazione dinamica è regolata dall'**effetto di accoppiamento elettromeccanico $\kappa^2$**[cite: 309]:
$$\kappa^2 = \frac{\alpha^2}{\alpha^2 + k^{E}C^{S}} = \frac{d^2}{s^{E}\epsilon^{T}}$$

Dato che il PZT-5H possiede un elevato fattore $\kappa^2$[cite: 158], la scelta dell'interfaccia elettrica modifica in modo sensibile la frequenza di risonanza meccanica e lo smorzamento del braccio del grammofono, influenzando la tracciabilità della punta nei solchi del vinile.

### Limite Inferiore della Risposta in Frequenza (I Toni Bassi)
Poiché il sensore equivale elettricamente a una sorgente di carica racchiusa su una capacità $C^{T}$[cite: 297], la presenza di una resistenza di carico in parallelo $R_L$ (composta dall'impedenza d'ingresso dell'amplificatore audio e dalle resistenze di isolamento del PZT) introduce un comportamento intrinseco da **filtro passa-alto**. La costante di tempo del sistema è definita da:

$$\tau = R_L \cdot C^{T}$$

* **Risposta a bassa frequenza:** Se la puntina incontra una frequenza audio molto bassa (es. toni bassi o variazioni quasi statiche, $\omega \to 0$), la carica generata dall'effetto piezoelettrico si disperde attraverso $R_L$ prima di poter stabilizzare una tensione misurabile agli elettrodi. Di conseguenza, il pickup piezoelettrico non ha risposta in continua (DC, $0\text{ Hz}$) e subisce una forte attenuazione e distorsione di fase sotto la frequenza di taglio $f_L = \frac{1}{2\pi\tau}$.
* **Soluzione Progettuale:** Per estendere la risposta in frequenza verso il basso e preservare la fedeltà dei toni musicali più gravi, è fondamentale garantire un'impedenza d'ingresso dell'amplificatore estremamente elevata ($R_L > 1 \text{ M}\Omega$, tipicamente implementata tramite stadi d'ingresso a FET o configurazioni ad *Amplificatore di Carica*). Questo accorgimento massimizza la costante di tempo $\tau$, permettendo una lettura lineare e non attenuata delle cariche elettriche dinamiche generate dalle oscillazioni del braccio sul PZT.
