
# Utilizzo #

Creare un Gantt Chart di base

## Includere JSGantt CSS e Javascript ##
```html
<link href="jsgantt.css" rel="stylesheet" type="text/css"/>
<script src="jsgantt.js" type="text/javascript"></script>
```

## Creare un elemento div per contenere il gantt chart ##
```html
<div style="position:relative" class="gantt" id="GanttChartDIV"></div>
```

## Iniziare un blocco `<script>` ##
```html
<script type="text/javascript">
```

## Istanziare JSGantt usando GanttChart() ##
```javascript
var g = new JSGantt.GanttChart(document.getElementById('GanttChartDIV'), 'day');
```

Definizione del metodo: **GanttChart(_pDiv_, _pFormat_)**

| Parametro | Descrizione |
|:--------|:------------------------------------------------|
| _pDiv:_ | (obbligatorio) questo è un oggetto DIV creato in HTML |
| _pFormat:_ | (obbligatorio) usato per indicare se il grafico deve essere disegnato in formato "hour", "day", "week", "month", o "quarter" |

## Personalizzare l'aspetto usando i metodi di configurazione ##
vedi [Opzioni di Configurazione](#opzioni) qui sotto

## Aggiungere Attività (Tasks) ##

### a) Usando il Metodo AddTaskItemObject() ###

```javascript

// passando un oggetto
g.AddTaskItemObject({
  "pID": 1,
  "pName": "Definire API del Grafico",
  "pStart": "2017-02-25",
  "pEnd": "2017-03-17",
  "pPlanStart": "2017-04-01",
  "pPlanEnd": "2017-04-15 12:00",
  "pClass": "ggroupblack",
  "pLink": "",
  "pMile": 0,
  "pRes": "Brian",
  "pComp": 0,
  "pGroup": 1,
  "pParent": 0,
  "pOpen": 1,
  "pDepend": "",
  "pCaption": "",
  "pCost": 1000,
  "pNotes": "Testo delle note"
});

// oppure passando parametri
g.AddTaskItem(new JSGantt.TaskItem(1, 'Definire API del Grafico','',          '',          'ggroupblack','', 0, 'Brian', 0,  1,0,1,'','','Testo delle note',g));
```


Definizione del metodo:
**TaskItem(_pID, pName, pStart, pEnd, pClass, pLink, pMile, pRes, pComp, pGroup, pParent, pOpen, pDepend, pCaption, pNotes, pGantt_)**

| Parametro | Descrizione |
|:--------|:------------------------------------------------|
|_pID:_|(obbligatorio) un ID numerico univoco usato per identificare ogni riga|
|_pName:_|(obbligatorio) l'etichetta dell'attività                               |
|_pStart:_|(obbligatorio) la data di inizio dell'attività, può essere vuota ('') per i gruppi. È anche possibile inserire un orario specifico (es. 2013-02-20 09:00) per maggiore precisione o mezze giornate|
|_pEnd:_|(obbligatorio) la data di fine dell'attività, può essere vuota ('') per i gruppi|
|_pPlanStart:_|(obbligatorio) la data di inizio pianificata dell'attività, può essere vuota ('') per i gruppi. È anche possibile inserire un orario specifico (es. 2013-02-20 09:00) per maggiore precisione o mezze giornate|
|_pPlanEnd:_|(obbligatorio) la data di fine pianificata dell'attività, può essere vuota ('') per i gruppi|
|_pClass:_|(obbligatorio) la classe CSS per questa attività                  |
|_pLink:_|(opzionale) qualsiasi link http da visualizzare nel tooltip come link "Più informazioni"|
|_pMile:_|(opzionale) indica se questa è un'attività milestone - Numerico; 1 = milestone, 0 = non milestone|
|_pRes:_|(opzionale) nome della risorsa                                |
|_pComp:_|(obbligatorio) percentuale di completamento, numerico                  |
|_pGroup:_|(opzionale) indica se questa è un'attività di gruppo (padre) - Numerico; 0 = attività normale, 1 = attività di gruppo standard, 2 = attività di gruppo combinata<sup>*</sup>|
|_pParent:_|(obbligatorio) identifica un pID padre, questo rende questa attività un figlio dell'attività identificata. Numerico, le attività di primo livello dovrebbero avere pParent impostato a 0|
|_pOpen:_|(obbligatorio) indica se un'attività di gruppo standard è aperta quando il grafico viene disegnato per la prima volta. Il valore deve essere impostato per tutti gli elementi ma è utilizzato solo dalle attività di gruppo standard.  Numerico, 1 = aperto, 0 = chiuso|
|_pDepend:_|(opzionale) elenco separato da virgole di id da cui questa attività dipende. Verrà disegnata una linea da ogni attività elencata a questo elemento. Ogni id può essere opzionalmente seguito da un suffisso di tipo di dipendenza. Valori validi sono: 'FS' - Fine a Inizio (predefinito se il suffisso è omesso), 'SF' - Inizio a Fine, 'SS' - Inizio a Inizio, 'FF' - Fine a Fine. Se presente, il suffisso deve essere aggiunto direttamente all'id, es. '123SS'|
|_pCaption:_|(opzionale) didascalia che verrà aggiunta dopo la barra dell'attività se CaptionType è impostato su "Caption"|
|_pNotes:_|(opzionale) informazioni dettagliate sull'attività che verranno visualizzate nel tooltip per questa attività|
|_pGantt:_|(obbligatorio) oggetto javascript JSGantt.GanttChart da cui prendere le impostazioni. Predefinito su "g" per retrocompatibilità|
|_pCost:_|(obbligatorio) costo di quell'attività, numerico        

<sup>*</sup> Le attività di gruppo combinate mostrano tutte le sotto-attività su una riga. Le informazioni visualizzate nell'elenco delle attività e nella didascalia della riga sono prese dall'attività padre. I tooltip sono generati individualmente per ogni sotto-attività dalle proprie informazioni. I milestone non sono validi come sotto-attività di un'attività di gruppo combinata e non verranno visualizzati. Non viene eseguito alcun controllo dei limiti delle date di inizio e fine delle sotto-attività, quindi è possibile che queste barre delle attività si sovrappongano. Le dipendenze possono essere impostate solo da e verso le sotto-attività.



### b) usando parseJSON() con un file JSON esterno o API ###
```javascript
JSGantt.parseJSON('./fixes/data.json', g);
```


La struttura del file JSON:
```json
{
  "pID": 1,
  "pName": "Definire API del Grafico",
  "pStart": "",
  "pEnd": "",
  "pPlanStart": "",
  "pPlanEnd": "",
  "pClass": "ggroupblack",
  "pLink": "",
  "pMile": 0,
  "pRes": "Brian",
  "pComp": 0,
  "pGroup": 1,
  "pParent": 0,
  "pOpen": 1,
  "pDepend": "",
  "pCaption": "",
  "pCost":  "",
  "pNotes": "Testo delle note"
}
```


### c) usando parseXML() con un file XML esterno ###
```javascript
JSGantt.parseXML("project.xml",g);
```

Definizione del metodo:
**JSGantt.parseXML(_pFile_, _pGanttObj_)**

| Parametro | Descrizione |
|:--------|:------------------------------------------------|
|_pFile:_|(obbligatorio) questo è il nome del file XML|
|_pGanttObj:_|(obbligatorio) un oggetto GanttChart restituito da una chiamata a JSGantt.GanttChart()|

La struttura del file XML nativo:
```xml
<project>
<task>
	<pID>25</pID>
	<pName>Modifiche WCF</pName>
	<pStart></pStart>
	<pEnd></pEnd>
  <pPlanStart></pPlanStart>
	<pPlanEnd></PlanEnd>
	<pClass>gtaskred</pClass>
	<pLink></pLink>
	<pMile>0</pMile>
	<pRes></pRes>
	<pComp>0</pComp>
	<pGroup>1</pGroup>
	<pParent>2</pParent>
	<pOpen>1</pOpen>
  <pCost></pCost>
	<pDepend>2,24</pDepend>
	<pCaption>Una didascalia</pCaption>
	<pNotes>Testo - può includere HTML limitato</pNotes>
</task>
</project>
```

Le definizioni dei campi sono come descritto per i parametri di TaskItem sopra. L'elemento pClass è opzionale nei file XML e avrà come valore predefinito "ggroupblack" per le attività di gruppo, "gtaskblue" per le attività normali e "gmilestone" per i milestone. L'elemento pGantt non è richiesto per l'importazione XML.

JSGannt Improved testerà anche il file XML fornito per vedere se sembra essere in formato XML di Microsoft Project. In tal caso, verrà effettuato un tentativo di caricare il progetto. Questa funzionalità è sperimentale, l'importazione è del tipo "best effort" e non garantita. Una volta caricato, il progetto come interpretato da JSGantt Improved può essere estratto utilizzando i metodi di esportazione XML forniti.


### d) usando parseXMLString() con XML contenuto in un oggetto stringa javascript ###
```javascript
JSGantt.parseXMLString("<project><task>...</task></project>",g);
```

Definizione del metodo:
**JSGantt.parseXML(_pStr_, _pGanttObj_)**

| Parametro | Descrizione |
|:--------|:------------------------------------------------|
|_pStr:_|(obbligatorio) questa è una Stringa javascript contenente XML|
|_pGanttObj:_|(obbligatorio) un oggetto GanttChart restituito da una chiamata a JSGantt.GanttChart()|


L'XML fornito verrà analizzato esattamente allo stesso modo del contenuto di un file XML esterno e quindi deve corrispondere al formato descritto per parseXML sopra.


## Chiamare Draw() ##
```javascript
g.Draw();
```

## Aggiornare un Gantt Chart esistente ##

È anche possibile eliminare attività usando il metodo RemoveTaskItem().
```javascript
g.RemoveTaskItem(11);
```

Definizione del metodo:
**RemoveTaskItem(_pID_)**

| Parametro | Descrizione |
|:--------|:------------------------------------------------|
|_pID:_|(obbligatorio) l'ID numerico univoco dell'elemento da rimuovere|

Se l'attività rimossa è un elemento di gruppo, verranno rimosse anche tutte le attività figlie.

Dopo aver aggiunto o rimosso attività, è necessario chiamare "g.Draw()" per ridisegnare il grafico.

# Opzioni #

È possibile impostare le Opzioni come un oggetto, seguendo l'esempio:

```javascript

g.setOptions({
  vCaptionType: 'Complete',       
  vQuarterColWidth: 36,
  vLang: 'it'
});

```

## Interruttori ##
Molte delle funzionalità di jsGanttImproved possono essere personalizzate attraverso l'uso di metodi setter disponibili sull'oggetto GanttChart restituito da una chiamata a JSGantt.GanttChart()
Le seguenti opzioni prendono un singolo parametro numerico; un valore di 1 abiliterà la funzionalità descritta, 0 la disabiliterà

| Metodo | Descrizione |
|:--------|:------------------------------------------------|
|_setUseToolTip():_|Controlla la visualizzazione dei tooltip, predefinito su 1 (abilitato)|
|_setUseFade():_   |Controlla l'uso dell'effetto dissolvenza quando si mostrano/nascondono i tooltip, predefinito su 1 (abilitato)|
|_setUseMove():_   |Controlla l'uso dell'effetto scorrimento quando si cambia tra diversi tooltip delle attività, predefinito su 1 (abilitato)|
|_setUseRowHlt():_ |Controlla l'uso dell'evidenziazione della riga al passaggio del mouse, predefinito su 1 (abilitato)|
|_setUseSort():_   |Controlla se l'elenco delle attività è ordinato in ordine di attività padre / ora di inizio o è semplicemente visualizzato nell'ordine di creazione, predefinito su 1 (ordinamento abilitato)|
|_setShowRes():_   |Controlla se la colonna Risorsa è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowDur():_   |Controlla se la colonna Durata Attività è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowComp():_  |Controlla se la colonna Percentuale Completamento è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowStartDate():_|Controlla se la colonna Data Inizio Attività è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowEndDate():_|Controlla se la colonna Data Fine Attività è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowPlanStartDate():_|Controlla se la colonna Data Inizio Pianificata dell'Attività è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowPlanEndDate():_|Controlla se la colonna Data Fine Pianificata dell'Attività è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowCost():_|Controlla se la colonna Costo è visualizzata nell'elenco delle attività, predefinito su 1 (mostra colonna)|
|_setShowTaskInfoRes():_|Controlla se le informazioni sulla Risorsa sono visualizzate nel tooltip dell'attività, predefinito su 1 (mostra informazioni)|
|_setShowTaskInfoDur():_|Controlla se le informazioni sulla Durata Attività sono visualizzate nel tooltip dell'attività, predefinito su 1 (mostra informazioni)|
|_setShowTaskInfoComp():_|Controlla se le informazioni sulla Percentuale Completamento sono visualizzate nel tooltip dell'attività, predefinito su 1 (mostra informazioni)|
|_setShowTaskInfoStartDate():_|Controlla se le informazioni sulla Data Inizio Attività sono visualizzate nel tooltip dell'attività, predefinito su 1 (mostra informazioni)|
|_setShowTaskInfoEndDate():_|Controlla se le informazioni sulla Data Fine Attività sono visualizzate nel tooltip dell'attività, predefinito su 1 (mostra informazioni)|
|_setShowTaskInfoLink():_|Controlla se il link Più Informazioni è visualizzato nel tooltip dell'attività, predefinito su 0 (NON mostrare link)|
|_setShowTaskInfoNotes():_|Controlla se i dati delle Note Aggiuntive sono visualizzati nel tooltip dell'attività, predefinito su 1 (mostra note)|
|_setShowEndWeekDate():_|Controlla se l'intestazione principale nella vista "Giorno" visualizza la data di fine settimana nel formato appropriato, predefinito su 1 (mostra data)|
|_setShowDeps():_  |Controlla la visualizzazione delle linee di dipendenza, predefinito su 1 (mostra dipendenze)|

## Valori Chiave ##
Le seguenti opzioni abilitano funzionalità usando un insieme di valori chiave specifici

| Metodo | Descrizione |
|:--------|:------------------------------------------------|
|_setShowSelector():_|Controlla dove è visualizzato il selettore di formato, accetta più parametri. I valori dei parametri validi sono "Top", "Bottom". Predefinito su "Top".|
|_setFormatArr():_   |Controlla quali opzioni di formato sono mostrate nel selettore di formato, accetta più parametri. I valori dei parametri validi sono "Hour", "Day", "Week", "Month", "Quarter". Predefinito su tutti i valori validi.|
|_setCaptionType():_ |Controlla quale campo dell'attività utilizzare come didascalia sulla barra delle attività del Gantt Chart, accetta un singolo parametro. I valori dei parametri validi sono "None", "Caption", "Resource", "Duration", "Complete". Predefinito su "None"|
|_setDateInputFormat():_|Definisce il formato di input utilizzato per le date nella creazione delle attività, accetta un singolo parametro. I valori dei parametri validi sono "yyyy-mm-dd", "dd/mm/yyyy", "mm/dd/yyyy". Predefinito su "yyyy-mm-dd"|
|_setScrollTo():_    |Imposta la data a cui il Gantt Chart verrà fatto scorrere, specificata nel formato di input della data impostato da setDateInputFormat() sopra. Accetta anche il valore speciale "today". Predefinito sulla data minima di visualizzazione|
|_setUseSingleCell():_|Imposta la soglia del numero totale di celle alla quale l'elenco delle attività utilizzerà una singola cella di tabella per ogni riga anziché una cella per periodo. Utile per migliorare le prestazioni su grafici di grandi dimensioni. Numerico, un valore di 0 disabilita questa funzionalità (usa sempre più celle), predefinito su 25000|
|_setLang():_        |Imposta la traduzione da utilizzare quando si disegna il grafico. Predefinito su "en" poiché questa è l'unica lingua fornita nell'installazione di base. Per usare l'italiano, impostare su "it"|

## Layout ##
La maggior parte dell'aspetto del Gantt Chart può essere controllata usando CSS, tuttavia, poiché la lunghezza di una barra delle attività è determinata dalla larghezza della colonna, i seguenti metodi prendono un singolo parametro numerico che definisce la larghezza della colonna appropriata in pixel.
Si noti che il codice di dimensionamento della barra delle attività assume l'uso di bordi di tabella compressi larghi 1px.

| Metodo | Descrizione |
|:--------|:------------------------------------------------|
|_setHourColWidth():_|Larghezza delle colonne del Gantt Chart in pixel quando disegnato in formato "Ora". Predefinito su 18.|
|_setDayColWidth():_ |Larghezza delle colonne del Gantt Chart in pixel quando disegnato in formato "Giorno". Predefinito su 18. |
|_setWeekColWidth():_|Larghezza delle colonne del Gantt Chart in pixel quando disegnato in formato "Settimana". Predefinito su 36.|
|_setMonthColWidth():_|Larghezza delle colonne del Gantt Chart in pixel quando disegnato in formato "Mese". Predefinito su 36.|
|_setQuarterColWidth():_|Larghezza delle colonne del Gantt Chart in pixel quando disegnato in formato "Trimestre", anche se non obbligatorio si raccomanda che questo sia impostato su un valore divisibile per 3. Predefinito su 18.|
|_setRowHeight():_|Altezza delle righe del Gantt Chart in pixel. Utilizzato per instradare le linee di dipendenza vicino ai punti finali. Predefinito su 20.|
|_setMinGpLen():_    |Le attività di gruppo hanno le loro barre delle attività abbellite con punti finali, questo valore specifica la larghezza di uno di questi punti finali in pixel. La lunghezza di una barra di attività corta verrà arrotondata per eccesso per visualizzare correttamente un singolo o entrambi i punti finali. Predefinito su 8.|

## Formati di Visualizzazione delle Date ##
I formati di visualizzazione delle date possono essere controllati individualmente. I metodi usati per impostare questi formati di visualizzazione prendono ciascuno un singolo parametro stringa di formato. La stringa di formato può essere composta dai seguenti componenti (sensibili alle maiuscole/minuscole)

| Componente | Descrizione |
|:--------|:------------------------------------------------|
|_h_|Ora (1-12)|
|_hh_|Ora (01-12)|
|_pm_|indicatore am/pm|
|_PM_|indicatore AM/PM|
|_H_|Ora (0-23)|
|_HH_|Ora (01-23)|
|_mi_|Minuti (1-59)|
|_MI_|Minuti (01-59)|
|_d_|Giorno (1-31) |
|_dd_|Giorno (01-31)|
|_day_|Abbreviazione del giorno della settimana|
|_DAY_|Giorno della settimana|
|_m_|Mese (1-12)|
|_mm_|Mese (01-12)|
|_mon_|Abbreviazione del testo del mese|
|_month_|Testo completo del mese|
|_yy_|Anno, escluso il secolo|
|_yyyy_|Anno       |
|_q_|Trimestre (1-4)|
|_qq_|Trimestre (Q1-Q4)|
|_w_|Numero settimana ISO (1-53)|
|_ww_|Numero settimana ISO (01-53)|
|_week_|Formato data settimana ISO completo|

separati da uno dei seguenti caratteri: **"/\-.,'`<spazio`>:**

Qualsiasi testo tra i separatori che non corrisponde a uno dei componenti sopra verrà controllato usando una corrispondenza insensibile alle maiuscole/minuscole per una stringa internazionalizzata valida. Se il valore non viene ancora trovato, il testo verrà emesso invariato.

I metodi di visualizzazione delle date disponibili sono

| Metodo | Descrizione |
|:--------|:------------------------------------------------|
|_setDateTaskTableDisplayFormat():_|Formato data usato per le date di inizio e fine nell'elenco principale delle attività. Predefinito su 'dd/mm/yyyy'.|
|_setDateTaskDisplayFormat():_     |Formato data usato per le date di inizio e fine nei tooltip delle attività. Predefinito su 'dd month yyyy'. |
|_setHourMajorDateDisplayFormat()_ |Formato data usato per le intestazioni delle date principali del Gantt Chart visualizzate in formato "Ora". Predefinito su 'day dd month yyyy'.|
|_setDayMajorDateDisplayFormat():_ |Formato data usato per le intestazioni delle date principali del Gantt Chart visualizzate in formato "Giorno". Predefinito su 'dd/mm/yyyy'.|
|_setWeekMajorDateDisplayFormat():_|Formato data usato per le intestazioni delle date principali del Gantt Chart visualizzate in formato "Settimana". Predefinito su 'yyyy'.|
|_setMonthMajorDateDisplayFormat():_|Formato data usato per le intestazioni delle date principali del Gantt Chart visualizzate in formato "Mese". Predefinito su 'yyyy'.|
|_setQuarterMajorDateDisplayFormat():_|Formato data usato per le intestazioni delle date principali del Gantt Chart visualizzate in formato "Anno". Predefinito su 'yyyy'.|
|_setHourMinorDateDisplayFormat()_ |Formato data usato per le intestazioni delle date secondarie del Gantt Chart visualizzate in formato "Ora". Predefinito su 'HH'.|
|_setDayMinorDateDisplayFormat():_ |Formato data usato per le intestazioni delle date secondarie del Gantt Chart visualizzate in formato "Giorno". Predefinito su 'dd'.|
|_setWeekMinorDateDisplayFormat():_|Formato data usato per le intestazioni delle date secondarie del Gantt Chart visualizzate in formato "Settimana". Predefinito su 'dd/mm'.|
|_setMonthMinorDateDisplayFormat():_|Formato data usato per le intestazioni delle date secondarie del Gantt Chart visualizzate in formato "Mese". Predefinito su 'mon'.|
|_setQuarterMinorDateDisplayFormat():_|Formato data usato per le intestazioni delle date secondarie del Gantt Chart visualizzate in formato "Anno". Predefinito su 'qq'.|

## Internazionalizzazione ##
jsGanttImproved fornisce solo testo in inglese, tuttavia tutte le stringhe codificate possono essere sostituite chiamando il metodo addLang() disponibile sull'oggetto GanttChart restituito da una chiamata a JSGantt.GanttChart()

Il metodo addLang() prende due parametri. Il primo è un identificatore di stringa per la lingua, il secondo è un oggetto javascript contenente tutte le coppie di testo sostitutivo.

**Per usare l'italiano, la traduzione è già inclusa nella libreria. Basta impostare:**

```javascript
g.setOptions({
  vLang: 'it'
});
```

Una volta impostata una traduzione, è necessario chiamare setLang() con l'identificatore di lingua appropriato prima di chiamare Draw().

## Esempio di Opzioni ##

Le opzioni di configurazione usate nel file index di esempio fornito sono:

```javascript

g.setOptions({
  vCaptionType: 'Complete',  // Impostare per mostrare la didascalia: None,Caption,Resource,Duration,Complete,     
  vQuarterColWidth: 36,
  vDateTaskDisplayFormat: 'day dd month yyyy', // Mostrato nel tooltip
  vDayMajorDateDisplayFormat: 'mon yyyy - Week ww',// Imposta il formato per visualizzare le date nell'intestazione "Principale" della vista "Giorno"
  vWeekMinorDateDisplayFormat: 'dd mon', // Imposta il formato per visualizzare le date nell'intestazione "Secondaria" della vista "Settimana"
  vLang: 'it',
  vShowTaskInfoLink: 1, // Mostra link nel tooltip (0/1)
  vShowEndWeekDate: 0,  // Mostra/Nascondi la data per l'ultimo giorno della settimana nell'intestazione per la vista giornaliera (1/0)
  vUseSingleCell: 10000, // Imposta la soglia alla quale useremo solo una cella per riga di tabella (0 disabilita). Aiuta con le prestazioni di rendering per grafici di grandi dimensioni.
  vFormatArr: ['Day', 'Week', 'Month', 'Quarter'], // Anche con setUseSingleCell l'uso del formato Ora su un grafico così grande può causare problemi in alcuni browser
});

```

# Esportazione XML #

I seguenti metodi possono essere utilizzati per estrarre i dettagli delle attività nel progetto in formato XML

Definizione del metodo: **getXMLProject()**

Restituisce una stringa contenente l'intero progetto in formato XML di JSGantt Improved. Le date verranno esportate nel formato di input attualmente definito come impostato da setDateInputFormat().

Definizione del metodo: **getXMLTask(_pID_, _pIdx_)**

| Parametro | Descrizione |
|:--------|:------------------------------------------------|
| _pID:_ | (obbligatorio) l'ID numerico che identifica l'attività da estrarre |
| _pIdx:_ | (opzionale) Booleano - se presente e impostato su "true" il numero passato nel parametro pID viene trattato come un indice dell'array per l'elenco delle attività anziché un ID |

Restituisce una stringa contenente l'elemento attività specificato in formato XML di JSGantt Improved. Le date verranno esportate nel formato di input attualmente definito come impostato da setDateInputFormat().
