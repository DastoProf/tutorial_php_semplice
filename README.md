# PHP

Il php (Hypertext Preprocessor) è un linguaggio **interpretato**. L'interprete degli script php è un programma chiamato `php`. 

Essendo che gli script php risiedono su un computer remoto, occorre che in questo computer vi sia un'altro programma chiamato **server process** che stia in ascolto delle richieste remote e richiami l'interprete php quando arriva una richiesta. Un tale server process potrebbe essere `Apache`. 

In realtà è possibile installare questi software su qualsiasi pc e farli funzionare in locale, facendo partire delle richieste indirizzate alla macchina in uso (indirizzo di loopback). Questa possibiltà risulta comoda in fase di sviluppo. Onde evitare di installare e configurare questi software singolarmente, conviene scaricare ed installare un pacchetto che li contiene e li gestisce all'unisono. Si tratta di `XAMPP`.

## Il primo script php
- Dirigiamoci nella cartella di installazione di XAMPP. Entriamo dunque nella cartella `htdocs` e creiamo una cartella o un percorso di cartelle dentro cui salvare lo script. Nel mio caso il percorso che ho creato è `C:\xampp\htdocs\my_projects\tutorial_1`. Stiamo attenti a non inserire spazi nei nomi delle cartelle, poichè ciò può impedire la corretta comunicazione tra browser (client) e Apache (server). 

- Dunque creiamo un file chiamato `index.php` ed apriamolo con qualsiasi editor. Al suo interno scriviamo il seguente codice
``` php
<?php
    echo "output del primo script php";
?>
```
- salviamo.

- Apriamo il pannello di controllo di XAMPP ed avviamo il server process Apache cliccando sul relativo pulsante di start.

- Apriamo una finestra del browser e digitiamo `localhost/percorso_file/index.php`. 
![Screenshot dell'output](/res/php_output_1.png)

### analisi del codice
uno script php si apre con il tag `<?php` e si chiude con `?>`. Tutto ciò che c'è tra questi tag, viene letto ed eseguito dall'interprete php. L'interprete valuta ogni istruzione e costruisce un file di testo, contentente al posto delle istruzioni php il risultato delle suddette istruzioni. Il server Apache preleva questo file e lo invia al browser che ne visualizza il contenuto.

La keyword `echo` provoca l'inserimento di una stringa nel file di output. Si noti che le istruzioni php terminano col `;`

>Approfondimento: Il codice va nella cartella `htdocs` perchè è quella a cui il server Apache ha accesso nella sua configurazione di default. Infatti apache non può fornire delle risorse salvate in percorsi a cui non ha accesso.

>Approfondimento: il file chiamato `index.php` è quello che il server fornisce automaticamente se non viene specificato altro dopo il percorso di cartelle.
# php e HTML
Il codice php può anche essere **embeddato** (incorporato) nei files HTML. 

- Nello stesso percorso dell'esercizio precedente o in uno nuovo (ma sempre nella cartella `htdocs`) si crei un file chiamato `example2.php`. 

Nonostante il file abbia del contenuto HTML, l'interprete php richiede che l'estensione sia `.php` per sapere che c'è del codice php da interpretare. 

- si inserisca il seguente contenuto
``` php
<!DOCTYPE html>
<html>
    <head>
        <title>Esempio 2</title>
    </head>

    <body>
        <h1>Il mio secondo script php</h1>

        <?php
            echo "<h2>è molto splendido :)</h2>";
        ?>
    </body>
</html>
```
- dopo aver salvato, si apra il browser e si inserisca l'URL `localhost/percorso/example2.php`
![Screenshot dell'output](/res/php_output_2.png)

L'interprete **parsa**<sub>(dall'inglese "to parse" ossia "analizzare")</sub> solo la porzione di codice racchiusa tra i tag di apertura e chiusura di php, lasciando il resto invariato.

In realtà è possibile avere più di una porzione di codice php in una pagina HTML. Questo perchè si vuol far calcolare dinamicamente a php il contenuto, in più punti della pagina separati.

- si modifichi il file `example2.php` come segue
```php
<!DOCTYPE html>
<html>
    <head>
        <title>Esempio 2</title>
    </head>

    <body>
        <h1>Il mio secondo script php</h1>

        <?php
            echo "<h2>è molto splendido :)</h2>";
        ?>
        <p>
            L'acqua del mare delle isole eolie ha una 
            salinità maggiore rispetto a quella dei mari con salinità minore.
        </p>
        <?php
            echo "<p>La salinità è ",3*3,"</h2>";
        ?>
    </body>
</html>
```
- si ricarichi la finestra del browser

![Screenshot dell'output](/res/php_output_3.png)

Si ponga attenzione sull'istruzione `echo "<p>La salinità è ",3*3,"</h2>";`. Da qua è possibile trarre un'approfondimento sulla sintassi di `echo`.Infatti dalla documentazione ufficiale si evince che è possibile dare in input alla funzione `echo` più parametri separati da virgola. In particolare come secondo parametro è stato dato un calcolo numerico, ma la funzione, dopo averlo svolto lo ha trasformato in stringa letterale e lo ha congiunto con le altre stringhe, formando la seguente istruzione HTML: `<p>La salinità è 9</h2>`.

# Variabili

Possiamo immaginare una variabile come una scatola vuota. in questa scatola ci possiamo mettere un numero, una lettera, o un'altro elemento computabile. In php una variabile viene **dichiarata** nel seguente modo: `$nome_variabile`. 

è importante che il nome cominci con una lettera o con underscore ( _ ) e non con un numero. Inoltre non può contenere spazi.

>Dichiarare una variabile vuol dire ordinare a php di riservargli un certo spazio in memoria che sarà occupato col **valore** della variabile, quando gli verrà **assegnato** per mezzo dell'_operatore_ `=`

>Assegnare un valore ad una variabile vuol dire scrivere nella memoria dedicata alla variabile, il valore che gli si assegna.

## script php con variabili
- in una nuova cartella dentro `htdocs` si crei un file `.php`.
- si inserisca il seguente codice
```php
<!DOCTYPE html>
<html>
<head>
    <title>Variabili in php</title>
</head>
<body>
    <h1>Esempio d'uso di variabili di tipo stringa</h1>
    <?php 
        $Island1 = "Salina";
        $Island2 = "Stromboli";
        echo "<p>La prima isola è $Island1 e la seconda è $Island2</p>";
    ?>
    <h1>Esempio d'uso di variabili di tipo Numero Intero e Numero decimale</h1>
    <?php 
        $costo = 700;
        $iva = 0.22;
        echo "<p>Il prezzo da pagare è di euro  ".($costo+$costo*$iva)."</p>";
    ?>
</body>
</html>
```
- lo si richieda nel browser con l'apposito URL 

![Screenshot dell'output](/res/php_output_4.png)

si noti la porzione di codice `($costo+$costo*$iva)` ove è stato fatto un uso sapiente delle variabili numeriche per far calcolare a php un prezzo più iva. Il tutto concatenato alle altre parti dell'espressione per mezzo dell'operatore `.` (punto).

Si noti inoltre che nelle espressioni numeriche, la moltiplicazione (e la divisione) ha la precedenza sull'addizione (sottrazione).

> [!WARNING]
> I nomi delle variabili sono _case sensitive_. Vuol dire che $ISLAND è una variabile diversa da $IslaNd

## Le variabili... variano :smile:
- si modifichi il codice precedente come segue
```php
<!DOCTYPE html>
<html>
<head>
    <title>Variabili in php</title>
</head>
<body>
    <h1>Esempio d'uso di variabili di tipo Numero Intero e Numero decimale</h1>
    <?php 
        $costo = 700;
        $iva = 0.22;
        echo "<p>Il prezzo da pagare è di euro  ".($costo+$costo*$iva)."</p>";
    ?>
    <h1>Esempio di riassegnazione</h1>
    <p>Applichiamo uno sconto di 200 euro</p>
    <?php 
        $sconto = 200;
        $costo = $costo - $sconto;
        echo "<p>Il prezzo scontato è di euro ".($costo+$costo*$iva)."</p>";
    ?>
</body>
</html>
```
- lo si esegua

![Screenshot dell'output](/res/php_output_5.png)

Da notare due cose:
- le variabili dichiarate in una certa porzione di php, sono ancora accessibili nelle porzioni successive.
- è possibile modificare il contenuto di una variabile (quindi farla variare) con una semplice riassegnazione (`$nome_var = <nuovo valore>`).
- nella riassegnazione la variabile può richiamare se stessa a destra dell'operatore `=` (es. ` $costo = $costo - $sconto;`). In questo caso il valore a destra dell'espressione è il vecchio. Infatti php prima calcola l'espressione col vecchio valore e poi effettua la nuova assegnazione.

>fino a questo punto di questa guida alle variabili è sempre stato assegnato un valore al momento della **Dichiarazione**. Ma è possibile dichiarare delle variabili vuote. In genere è però sconsigliato.

# Costanti
Se una variabile la si può immaginare come una scatola aperta a cui è possibile cambiare il contenuto, una costante è una scatola chiusa a cui non è possibile cambiare il contenuto.

La sintassi per dichiarare una variabile è `define("CONST_NAME",  "Valore o frase che non cambia")`
Per convenzione il nome delle costanti è tutto in maiuscolo e segue le stesse regole del nome delle variabili (non può iniziare con un numero).

## Esempio pratico di utilizzo di costanti
- creiamo un nuovo file php e inseriamo il seguente contenuto
```php
<!DOCTYPE html>
<html>
<head>
    <title>Costanti in php</title>
</head>
<body>
    <h1>Esempio d'uso di costante di tipo Numerico</h1>
    <?php 
        define("PI_GREEK", 3.14);
        $raggio = 4;
        echo "<p>La circonferenza del cerchio di raggio $raggio è  ".($raggio*2*PI_GREEK)."</p>";
        $raggio = 7;
        echo "<p>La circonferenza del cerchio di raggio $raggio è  ".($raggio*2*PI_GREEK)."</p>";
        $raggio = 15;
        echo "<p>La circonferenza del cerchio di raggio $raggio è  ".($raggio*2*PI_GREEK)."</p>";
    ?>
</body>
</html>
```
- lo si mandi in esecuzione

![Screenshot dell'output](/res/php_output_6.png)

mentre è possibile riassegnare la variabile `$raggio`, tentare di riassegnare un altro numero a `PI_GREEK` darebbe un errore. Questo ne aumenta la sicurezza, visto che l'obiettivo delle costanti è appunto _rimanere costanti_ .

# Tipi delle variabili
Adesso passiamo alla rassegna i principali tipi di variabile (ma non tutti). Il tipo della variabile informa php su che tipo di valore contiene la variabile.
## String
Abbiamo già usato delle variabili con qusto tipo. Una Stringa è una serie di caratteri racchiusi tra virgolette.

`$Island1 = "Salina"` è una variabile di tipo stringa, perchè il valre che contiene (ossia `"Salina"`) è una stringa.

## Integer
Anche questo tipo di variabile lo conosciamo già. Una variabile Integer è una variabile che contiene un numero intero (ossia senza virgola) sia positivo che negativo.

`$costo = 700` è un esempio di variabile Integer.

## Float
Sta per Floating Point Number, ossia numero a virgola mobile. Le variabili di questo tipo sono infatti quelle che contengono numeri con la virgola.

`$iva = 0.22` è un esempio di variabile Float. 
>Si noti come il separatore decimale è però il punto e non la virgola.

## Boolean
Un variabile booleana può assumere uno solo tra due valori. questi 2 valori sono Vero `true` o Falso `false`. 

`$iva_applicabile = false` è un esempio di variabile booleana. La loro utilità sarà più chiara quando affronteremo le istruzioni condizionali. Ossia porzioni di codice che vengono eseguite solo se una qualche variabile booleana ha valore `true`, ma non se ha valore `false`.

## NULL
Una variabile che questo tipo, è una variabile che non ha nessun valore assegnato. Se si dichiara una variabile senza assegnargli un valore, quella sarà una variabile che contiene il valore `NULL`, e il suo tipo è appunto NULL.

```php
//...codice precedente
$variabile_null;
//resto del codice...
```
è un esemio di variabile NULL.

Tuttavia, una variabile che ha un valore assegnato, si può svuotare assegnandogli il valore `null` e rendendola dunque di tipo NULL

```php
//..codice precedente
$x = "Hello world!";
$x = null;
//resto del codice...
```

# Commenti
Può capitare che un'altro programmatore debba modificare il nostro codice, ma non riesce a capire esattamente come funziona e cosa fa ogni singola istruzione. Inoltre anche noi stessi dopo un po di tempo possiamo dimenticare cosa faceva il codice che abbiamo scritto tempo addietro. In questi casi tornano utili i commenti. Si tratta di linee di testo che l'interprete php ignora. Infatti servono solo per essere letti dagli umani.
```php
<?php
// questo è un commento su una linea

# questo pure

$costo = 30;
$iva = 0.22;

//la variabile dubbia qui sotto serve per calcolare il prezzo con iva
$variabile_dubbia = $costo*(1+$iva);
?>
```

```php
<?php
/*
questo è un commento su più linee
che serve ad avere
un commento su più righe
*/
    echo "Hello !"; 
?>
```
I commenti vengono anche sfruttati per disabilitare delle linee di codice senza cancellarle. Infatti come si è detto le linee di commento vengono ignorate da php e quindi non eseguite.
```php
<?php
    //echo "Hello Salina!";
    echo "Hello Lipari!";
?>
```

# Le Funzioni
Può capitare di dover scrivere un cero numero di istruzioni più di una volta al fine di ottenere un certo risultato. Queste istruzioni sono sempre le stesse e fanno sempre la stessa cosa, come calcolare un prezzo, una misura etc. Oppure semplicemente mandano in output qualcosa. 

Le funzioni sono dei blocchi di codice che fanno appunto qualcosa che serve fare spesso. Invece di fare sempre copia e incolla del codice, basta scrivere solo il nome della funzione e il blocco di codice (scritto una volta sola) viene eseguito.
## sintassi delle funzioni
```php
function functionName(...$arguments) {
  code to be executed;
}
```
## esempio pratico
```php
<!DOCTYPE html>
<html>
<head>
    <title>Funzioni in php</title>
</head>
<body>
    <?php 
        function salutaIsola($nomeIsola){
            echo "<h1>Ciao $nomeIsola !</h1>";
        }

        salutaIsola("Lipari");
        salutaIsola("Vulcano");
        salutaIsola("Filicudi");
    ?>
</body>
</html>
```
![Screenshot dell'output](/res/php_output_7.png)

## come funzionano le funzioni?
![Screenshot dell'output](/res/funzione.png)
Una funzione è come un macchinario. Gli si danno in pasto dei valori, la funzione li elabora eseguendo il codice tra parentesi graffe e fornisce in output il risultato dell'elaborazione.

In realtà esistono funzioni che non hanno bisogno di valori di input e funzioni che non forniscono nessun valore di output. Infatti la funzione dell'esempio sopra, esegue il codice tra parentesi graffe e non prevede valori di output.

In particolare, nell'esempio ogni volta che viene chiamata la funzione, viene eseguito il codice in essa definito. Si noti che cambiare il valore dell'input, vuol dire assegnare un valore diverso all'**argomento** `$nomeIsola`. Questo argomento viene trattato dal codice della funzione come una normale variabile.

## Funzioni con valore di ritorno
Una funzione può essere chiamata in un **espressione** ove giova il suo risultato o valore di ritorno (se la funzione lo prevede).
si osservi il seguente esempio:
```php
<!DOCTYPE html>
<html>
<head>
    <title>Funzioni con return</title>
</head>
<body>
    <?php 
        function calcolaAreaCerchio($raggio){
            $area = 3.14*$raggio*$raggio; //questa variabile non è accessibile da fuori la funzione
            return $area;
        }

        $raggio = 5; //questa variabile non è accessibile da dentro la funzione
        $altezza = 7;
        echo "<p>Il volume del cilindro con cerchio di base di raggio $raggio e altezza $altezza è pari a </p>";
        
        echo calcolaAreaCerchio($raggio)*$altezza;
    ?>
</body>
</html>
```
![Screenshot dell'output](/res/php_output_8.png)

Come si osserva, la funzione ha delle istruzioni che servono a calcolare un'area e ritorna in output il valore calcolato per mezzo dell'istruzione `return <valore di output>`. Quando php incontra la chiamata alla funzione nella riga `echo calcolaAreaCerchio($raggio)*$altezza;`, quello che fa è eseguire la funzione, sostituire il valore ritornato al posto della chiamata e calcolare l'espressione (che diventerà `echo 78.5*7;`).  

# Scope delle variabili
lo **scope** di una variabile è la parte dello script dove la variabile può essere usata.
In php ci sono 3 scopes:
1. local
1. global
1. static
## local
Una variabile dichiarata dentro una funzione ha scope local, ed è accessibile solo da dentro la funzione. Provare a modificarla da fuori il blocco della funzione non funzionerà. 
```php
<?php
function myTest() {
  $x = 5; // local scope
  echo "<p>Variable x inside function is: $x</p>";
}
myTest();

// using x outside the function will generate an error
echo "<p>Variable x outside function is: $x</p>";
?>
```
## global 
Una variabile dichiarata al di fuori di qualsiasi funzione ha scope global ed è accessibile solo al di fuori delle funzioni. Provare a usarla dentro una fonzione darà errori.
```php
<?php
$x = 5; // global scope

function myTest() {
  // using x inside this function will generate an error
  echo "<p>Variable x inside function is: $x</p>";
}
myTest();

echo "<p>Variable x outside function is: $x</p>";
?>
```

Una variabile dichiarata dentro una funzione può avere lo stesso nome di una dichiarata al di fuori (come in qualche esempio fa con la variabile `$raggio`). Ma le due variabili sono diverse. La modifica dell'una non influenza l'altra.

## static
Normalmente, dopo che una funzione viene eseguita, le sue variabili locali vengono cancellate. Ma ogni tanto si desidera preservare queste variabili. Per farlo si usa la **keyword** `static`.
```php
<?php
function myTest() {
  static $x = 0;
  echo $x;
  $x++;
}

myTest();
myTest();
myTest();
?>
```
![Screenshot dell'output](/res/php_output_9.png)
ogni volta che la funzione viene richiamata, la variabile `$x` mantiene il valore che conteneva l'ultima volta che la funzione è stata eseguita.

## la keyword `global`
è usata per accedere alle variabili globali da dentro una funzione.
```php
<?php
$x = 5;
$y = 10;

function myTest() {
  global $x, $y;
  $y = $x + $y;
}

myTest();
echo $y; // outputs 15
?>
```
# La funzione var_dump()
Viene sfruttata per conoscere il tipo ed il valore di una variabile.
```php
<?php 
    $nome = "Augusto";
    $eta = 18;
    $diplomato = true;
    var_dump($nome);
    echo "<br>";
    var_dump($eta);
    echo "<br>";
    var_dump($diplomato);
?>
```
![Screenshot dell'output](/res/php_output_10.png)
# istruzioni condizionali
Può capitare di voler eseguire un blocco di codice **solo se** una certa condizione è vera. Per fare ciò si può usare l'istruzione `if`.
```php
<?php 
    echo "<p>Il tuo menu prevede lasagne</p>";

    $sgarroDay = true;

    if($sgarroDay){
        echo "<p>più Hamburgher patatine e bibite gassate</p>";
    }
?>
```
![Screenshot dell'output](/res/php_output_11.png)

Può capitare ancora di voler eseguire un blocco di codice se una certa condizione è vera, e di voler eseguire un'altro blocco di codice se è falsa. Per farlo all'`if` dovrà seguire l'`else`.
```php
<?php 
    echo "<p>Il tuo menu prevede lasagne</p>";

    $sgarroDay = false;

    if($sgarroDay){
        echo "<p>più Hamburgher patatine e bibite gassate</p>";
    }else{
        echo "<p>più insalata e acqua minerale</p>";
    }
?>
```
![Screenshot dell'output](/res/php_output_12.png)

Inoltre è possibile testare più di 2 condizioni, ed eseguire un blocco di codice a seconda di quale si verifica.
```php
<?php 
    echo "<h1>Vincita della sagra del paese</h1>";

    $etaVincitore = 19;

    if($etaVincitore < 14){
        echo "<p>Hai vinto una Bici</p>";
    }elseif($etaVincitore < 18){
        echo "<p>Hai vinto uno Scooter</p>";
    }else{
        echo "<p>Hai vinto un Aereo</p>";
    }
?>
```
Si osserva che qui non ci sono variabili booleane, ma dentro la parentesi dell'`if` c'è un'espressione. Il php esegue l'espressione e determina se è true o false, e di conseguenza esegue il blocco giusto. Ad esempio `$etaVincitore < 14` diventa `19 < 14` che è falso per cui il primo blocco non viene eseguito. lo stesso vale con il secondo. Infine resta il terzo che è dunque quello che viene eseguito.

# Operatori logici
Sono utilizzati per combinare espressioni condizionali.
- and: es. `$x and $y` risolve a true se $x e $y sono entrambe le variabili true. Oppure `$eta >10 and $eta < 20`. Oppure si può scrivere `$x && $y` più brevemente.
- or: es. `$x or $y` o equivalentemente `$x || $y` risolve a true se almeno una variabile è true.
- xor: es. `$x xor $y` risolve a true se una sola variabile è true, ma non l'altra.
- not: è la negazione del valore. es. `!$x` risolve a true se $x e false. Mentre risolve a false se $x è true.
# switch case
Ci sono dei casi in cui si vuole eseguire un blocco di codice se si verifica una consizione. Per fare questo abbiamo già introdotto il costrutto `if`. Ma se le condizioni che possono verificarsi sono più di due o tre non conviene usare l'`if`. Meglio usare il `switch`. 
```php
<?php 
    echo "<h1>Colore preferito</h1>";

    $colorePref = "magenta";

    switch($colorePref){
        case "rosso":
            echo "ti piace il rosso";
            break; 
        case "verde":
            echo "ti piace il verde";
            break;
        case "bianco":
            echo "ti piace il bianco";
            break;
        case "magenta":
            echo "ti piace il magenta";
            break; //senza il break verrebbe eseguito questo blocco e quelli seguenti
        case "blu":
            echo "ti piace il blu";
            break;
        default: //viene eseguito se non si trovano match
            echo "non ti piacciono i colori";
    }
?>
```
![Screenshot dell'output](/res/php_output_13.png)

il switch passa alla rassegna i vari `case`, e quando trova una corrispondenza tra il case e l'argomento passato in input esegue il codice relativo al case. `break` serve a dire al switch di fermarsi, altrimenti eseguirebbe anche i blocchi di codice dei casi successivi, anche se non corrispondono all'argomento. Se non viene trovata nessuna corrispondenza viene eseguito il codice dopo `default`. Quest'ultimo va scritto alla fine, dopo tutti i case. 

# Array
un array è un altro **tipo** di variabile che può contenere più di un valore. Una scatola di scatole.
```php
<?php 
    $destinazioni = array("Dublino", "cagliari", "Antofagasta", "Marrakech");
    $compagnie = ["RyanAir", "Ethiad", "AirOne", "Lufthansa"];
    echo "vado a $destinazioni[3] con la compagnia $compagnie[0]";
?>
```
Si osserva che vi sono due modi di assegnare i valori ad un array. Il primo è utilizzando la funzione `array()` ed il secondo è elencare gli elementi tra parentesi quadre. 

Gli elementi dell'array sono numerati a partire da 0. Per accedere ad un elemento si usa la sintassi `$nomeArray[<posizione elemento>]`. Per esempio la prima destinazione nel codice sopra la si ottiene con `$destinazioni[0]`.

![Screenshot dell'output](/res/php_output_14.png)

Gli arrai appena visti si chiamano _indexed array_ appunto per il fatto che ogni elemento ha un indice. Si può sfruttare l'indice dell'elemento anche per modificarne il valore.
```php
<?php 
    $destinazioni = array("Dublino", "cagliari", "Antofagasta", "Marrakech");
    $compagnie = ["RyanAir", "Ethiad", "AirOne", "Lufthansa"];
    $destinazioni[3] = "Sydney";
    echo "vado a $destinazioni[3] con la compagnia $compagnie[0]";
?>
```
![Screenshot dell'output](/res/php_output_15.png)

Abbiamo modificato l'elemento 3 delle destinazioni in Sydney.
## array associativi
Invece di usare i numeri per trovare gli elementi, vengono usati dei nomi chiamati **chiave dell'elemento**. Possono tornare utili in diverse occasioni. Ad esempio se si vogliono mappare dei nomi a dei valori numerici.
```php
<?php 
    $prezziAuto = array("Audi" => 40000, "Roll-Royce" => 150000, "Tesla" => 70000);
    echo "la tesla costa $prezziAuto[Tesla] euro </br>";
    echo "L'audi costa ".$prezziAuto['Audi']. " euro";
?>
```

Si nota come per accedere ai prezzi mappati ai nomi delle automobili, basta usare come indice il nome stesso della macchina.

![Screenshot dell'output](/res/php_output_16.png)
## array multidimensionali
Un array multidimensionale è un array che contiene altri array. Si possono avere array bi-dimensionali (array di array) array tri-dimensionali (array di array di array) etc. 
Si consideri la seguente tabella:
![Screenshot dell'output](/res/tab1.png)
possiamo notare che tolta l'intestazione, i dati si distribuiscono in 4 righe e 3 colonne. Possiamo immaginare la tabella come un array dove ogni riga è un elemento. A sua volta possiamo immaginare una riga come un array dove ogni valore di colonna è un elemento. Rappresentiamo dunque la tabella come array bi-dimensionale:
```php
<?php 
    $cars = array (
        array("Volvo",22,18),
        array("BMW",15,13),
        array("Saab",5,2),
        array("Land Rover",17,15)
      );
?>
```
A questo punto per accedere ad ogni elemento abbisognamo di due indici. Il primo indice si riferisce alla posizione dell'array riga da pescare. Il secondo indice si riferisce alla posizione dell'elemento da pescare dentro l'array riga prima selezionato. Se si vuole il primo indice è la riga ed il secondo la colonna.
```php
<?php 
    $cars = array (
        array("Volvo",22,18),
        array("BMW",15,13),
        array("Saab",5,2),
        array("Land Rover",17,15)
      );

      echo $cars[0][0].": In stock: ".$cars[0][1].", sold: ".$cars[0][2].".<br>";
      echo $cars[1][0].": In stock: ".$cars[1][1].", sold: ".$cars[1][2].".<br>";
      echo $cars[2][0].": In stock: ".$cars[2][1].", sold: ".$cars[2][2].".<br>";
      echo $cars[3][0].": In stock: ".$cars[3][1].", sold: ".$cars[3][2].".<br>";
?>
```
![Screenshot dell'output](/res/php_output_17.png)

# loop
Loop vuol dire ripetizione. Può capitare di voler eseguire lo stesso blocco di codice un certo numero di volte. Le funzioni questa volta non tornano utili perchè dovremmo richiamarle tante volte e magari con parametri diversi. i loop invece ci danno la possibilità di eseguire un certo blocco di codice finchè una certa condizione è vera.
## ciclo while
Esegue un blocco di codice **finche** una certa condizione specificata come argomento è vera.
```php
<?php 
$contatore = 1;
while($contatore < 5){
    echo "iterazione numero $contatore <br>";
    $contatore++; //equivale a $contatore = $contatore + 1
}
?>
```
![Screenshot dell'output](/res/php_output_18.png)

Il parser php verifica la condizione, se vera entra nel ciclo ed esegue le istruzioni. Tra le istruzioni c'è quella di incrementare il contatore. Finito il blocco di istruzioni il parser torna indietro e verifica sempre se la condizione è vera. Se lo è riesegue di nuovo il codice e ripete questo ciclo finchè non trova che la condizione è falsa. quando è falsa salta all'istruzione dopo del blocco while (nell'esempio non c'è più nessuna istruzione quindi il programma finisce).

## ciclo do...while
è come il ciclo while, solo che la condizione viene verificata alla fine dell'esecuzione del blocco e non all'inizio.
```php
<?php
    $contatore = 1;

    do{
        echo "iterazione numero $contatore <br>";
        $contatore++;
    }while($contatore < 5);

    echo "<br><br>";
    $contatore = 10;
    
    do{
        echo "iterazione numero $contatore <br>";
        $contatore++;
    }while($contatore < 5);//anche se la condizione è falsa , viene chekkata alla fine
?>
```
![Screenshot dell'output](/res/php_output_19.png)

## ciclo for
è una versione migliorata del ciclo while. Infatti se guardiamo l'esempio del ciclo while, quello che facevamo era dichiarare una variabile contatore, testare se assumeva un certo valore e ad ogni iterazione incrementarla. Il `for` consente di fare tutto questo in una sola riga.
```
for (init counter; test counter; increment counter) {
  code to be executed for each iteration;
}
```
- `init counter`: Inizializzazione del contatore
- `test counter`: testa la condizione per sapere se entrare nel ciclo
- `increment counter` : aumenta il contatore dopo ogni esecuzione del ciclo. Può in realtà aumentare di più di un unità e addirittura può anche diminuire.
```php
<?php 
    for($contatore = 0; $contatore < 10; $contatore+=2){
        echo "Il contatore ha valore $contatore <br>";
    }
    
    echo "ciclo al contrario <br>";

    for($contatore = 10; $contatore > 0; $contatore--){
        echo "Il contatore ha valore $contatore <br>";
    }
?>
```
![Screenshot dell'output](/res/php_output_20.png)

## ciclo foreach
foreach vuol dire per ogni. Quando si lavora con gli array, è possibile usare i cicli per eseguire un blocco di codice per ogni elemento contenuto nell'array e quindi fare qualcosa con l'elemento di volta in volta considerato.

Il ciclo foreach semplifica questa operazione grazie alla sua sintassi.
```php
<?php 
    $colori = ["arancione", "verde", "giallo"];

    echo "I colori nell'array sono: <br>";
    foreach($colori as $colore){
        echo "$colore <br>";
    }
?>
```
![Screenshot dell'output](/res/php_output_21.png)

nella riga `foreach($colori as $colore)` $colori è il nome dell'array, mentre $colore è il nome della variabile che di volta in volta conterrà l'elemento considerato. Agendo su $colore vuol dire quindi agire sull'elemento.

{esercizio: usare il ciclo foreach per rendere tutti gli elementi uppercase e un altro ciclo per stamparli

Hint: `foreach($array as &$element)` ove la `&` serve ad assegnare il valore dell'elemento alla variabile $element per **referenza** così che le modifiche agiranno sulla locazione di memoria dell'elemento e non su una copia dello stesso
}

la seguente invece è la sintassi per iterare sugli array associativi:
```php
<?php 
    $ages = array("Peter"=>"35", "Ben"=>"37", "Joe"=>"43");

    foreach($ages as $name => $val) {
        echo "$name = $val<br>";
    }
?>
```
quando scriviamo `foreach($ages as $name => $val)` vuol dire che `$name` conterrà la chiave dell'elemento e `$val` il suo valore.

![Screenshot dell'output](/res/php_output_22.png)

## break loop
abbiamo già visto che l'istruzione break ciconsente di uscire da un blocco switch. In realtà ci consente di uscire anche da un ciclo (while, do while, for, foreach). Vediamo l'esempio di come abbandonare il ciclo while quando il contatore raggiunge un certo valore.
```php
<?php 
    $contatore = 1;
    while($contatore < 10){
        echo "Iterazione numero $contatore <br>";
        if($contatore == 4){
            break;
        }
        $contatore++;
    }
    echo "qui siamo usciti fuori dal ciclo";
?>
``` 
![Screenshot dell'output](/res/php_output_23.png)

## continue loop
l'istruzione `continue` serve invece a saltare un'iterazione e passare alla successiva.
```php
<?php 
    $contatore = 1;
    while($contatore < 6){
        $contatore++;
        
        if($contatore == 4){
            continue;
        }
        echo "Iterazione numero $contatore <br>";
        //$contatore++;
    }
?>
```

Per non andare in un loop infinito si è spostati l'incremento del contatore prima del `continue`. Per apprezzare l'effetto del continue si è spostato il codice che deve essere salatato dopo del continue.

# Form
## gesione dei form
I form sono delle sezioni di una pagina web in cui l'utente inserisce dei dati. Una volta inseriti preme un bottone e i dati vengono inviati al server che li elabora per mezzo di uno script php.

Osserviamo una pagina HTML che contiene un form:
```html
<!DOCTYPE html>
<html>
<head>
    <title>php form</title>
</head>
<body>
    <form action="index.php" method="post">
        Nome: <input type="text" name="name"> <br>
        Email: <input type="email" name="email"> <br>
        <input type="submit" value="Invia al server">
    </form>
</body>
</html>
```
Dalla riga `<form action="index.php" method="post">` notiamo che l'attributo `action` del form punta ad uno script php. Si tratta dello script a cui sono destinati i dati. L'attribuot `method` invece ha il valore `POST`. Si tratta di una modalità di invio dei dati propria del protocollo di comunicazione **HTTP**, protocollo usato per comunicare col server. 

Notiamo i due elementi di input che raccolgono i dati utente
```html
Nome: <input type="text" name="name"> <br>
Email: <input type="email" name="email"> <br>
```
essi contengono un attributo `name` il cui valore sarà quello che consente allo script php di recuperare le informazioni in essi contenute.

`<input type="submit" value="Invia al server">` Quando viene premuto questo bottone, essendo il suo tipo "submit" partirà l'invio dei dati al server, e saranno gestiti dallo script specificato nel tag di apertura del form.

![Screenshot dell'output](/res/php_output_25.png)

Vediamo ora come lo script `index.php` a cui sono destinati i dati riesce a leggerli:

```php
<?php 
    echo "il tuo nome è $_POST[name] <br>";
    echo "la tua mail è $_POST[email]";
?>
```
Il metodo scelto per inviare i dati era il POST come abbiamo visto. I dati inviati vengono scritti nella variabile superglobale `$_POST` che altri non è che un array associativo. I nomi dei campi di input di cui si vuole recuperare il valore sono la chiave da inserire come indice nell'array &_POST. 

![Screenshot dell'output](/res/php_output_24.png)

--------------------------
Un altro modo per inviare dati al server tramite il form è l'uso del metodo GET. La differenza è che non è possibile con questo metodo mandare dati pesanti come files e immagini, ma solo brevi stringhe. Oltretutto i dati così inviati andranno ad essere mappati nell'URL che il browser costruisce quando fa partire la richiesta. Questo rappresenta un problema di sicurezza per i dati sensibili. 

Modifichiamo il codice precedente per farlo funzionare col metodo GET e vediamone gli effetti. Ecco il file home.html:
```html
<!DOCTYPE html>
<html>
<head>
    <title>php form</title>
</head>
<body>
    <form action="index.php" method="get">
        Nome: <input type="text" name="name"> <br>
        Email: <input type="email" name="email"> <br>
        <input type="submit" value="Invia al server">
    </form>
</body>
</html>
```
Come osserviamo nulla cambia se non che nella riga `<form action="index.php" method="get">` compare adesso il metodo GET.

Questa volta i dati inviati vengono scritti sulla variabile superglobale $_GET:
```php
<?php 
    echo "il tuo nome è $_GET[name] <br>";
    echo "la tua mail è $_GET[email]";
?>
```
 Inseriamo i dati nel form e facciamo partire la chiamata al server:
 ![Screenshot dell'output](/res/php_output_26.png)

 Come vediamo, il browser nel costruire l'URL per comunicare col server, ha aggiunto una parte: `?name=asda&email=asfa%40asd.it` chiamata **query string** che contiene le informazioni che l'utente ha inserito nel form. 