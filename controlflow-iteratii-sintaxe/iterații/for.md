# Enunțul for

Precum în cazul lui `while` sau al lui `do`, `for` execută repetat un fragment de cod de câte ori o condiție este întrunită.
Există o regulă simplă pe care o avem de la cercetătorul Edsger W. Dijkstra care spune așa:

> two or more, use a for

Se traduce în limba română *două sau ciopor, folosește for*.

Acest enunț, numit de standard `IterationStatement`, creează o secvență repetitivă de evaluare a unor expresii care produce un set de rezultate. Este enunțul cel mai des folosit pentru a genera serii de numere, pentru a prelucra seturi de valori din array-uri, pentru a asocia valori din liste diferite și cam tot ce îți trece prin minte atunci când vine vorba de a lucra cu intervale de numere sau seturi de date în general.

Înțelegerea iterațiilor cu `for` este pasul către înțelegerea unor instrumente mai puternice cum ar fi `Array.prototype.forEach()` și mai departe pentru `Array.prototype.map()`, `Array.prototype.reduce()` și `Array.prototype.filter()`.

## Bloc de inițializare și execuție

Buclele vor fi create ținându-se cont de câteva expresii opționale introduse între parantezele, așa-numitul **bloc de inițializare**. Urmează un **bloc de execuție**, care conține expresiile petru evaluare la fiecare pas al buclei.

### Despre intervale

Pentru a construi bucle for, avem nevoie să înțelegem că numărul de cicluri, de iterații, de bucle, este dat de un interval numeric pe care-l creăm de la bun început în **blocul de inițializare**. Acest interval este inițiat prin declararea unei variabile cu o valoare numerică - un **contor**. Apoi, este nevoie de specificarea limitei până la care se vor face iterații. Această limită poate fi una deschisă, dacă este folosit operatorul de comparare. Folosind mai mic sau mai mare după necesitate, indică motorului că este vizat un interval deschis, ce exclude și ultima valoare, dar dacă se folosește mai mic sau egal ori mai mare sau egal, motorul va ști că dorim folosirea unui interval închis. Ultima iterație va fi făcută chiar pe valoarea menționată la comparator.

Un interval care pornește de la 0 și are menționată limita ca fiind 3, în cazul folosirii operatorului de comparație simplu, va declanșa o buclă cu trei iterații: pentru 0, pentru 1, pentru 2, dar nu și pentru 3. Oarecum face sens deplin pentru că asta ne-am și dorit specificând valoarea 3: dorim trei iterații. Dacă foloseam operatorul de comparație combinat, care va include și valoarea trei, vom avea 4 iterații.

### Blocul de inițializare

Oricare dintre *expresiile opționale* pot fi utilizate sau nu în **blocul de inițializare**. Mai jos avem un exemplu pentru care s-a optat plasarea variabilei cu rol de contor în afara blocului de inițializare. Sintaxa este perfect legitimă atâta vreme cât pui totuși un punct și virgulă care să delimiteze *locul* contorului de expresia de comparare.

```javascript
var x = 0; // contor în afară
for (; x < 5; x++) {
  console.log(x);
};
```

Expresiile opționale sunt separate prin punct și virgulă și se compun din următoarele:

-   **un contor** care este o valoare prestabilită (standardul spune că este un `LexicalDeclaration Expression`);
-   **un comparator** care ia valoarea din contor și o compară cu o altă valoare, de regulă dimensiunea unui array adusă prin proprietatea `numeArray.length`;
-   **un incrementor/decrementor** care are rolul de a adăuga sau scădea la valoarea existentă a contorului.

Privind la expresiile folosite pentru a face funcțional un `for`, îți reamintește de `do...while` și te întrebi, de ce nu l-ai folosi în continuare pe aceasta. Diferența este că la `do...while`, inițializarea sau contorul (ca expresie) stă în blocul de cod ce trebuie executat, iar condiția sau comparatorul este în **blocul expresiei de evaluat**. În cazul lui `for`, blocul are la final expresia de incrementare. Opțiunea pentru `for` este concizia.

De cele mai multe ori vei întâlni în cod numele variabilei pentru contor drept litera `i`. Acesta vine ca prescurtare la termenul *index* și este larg utilizat. Atenție, nu este necesar să se folosească `i`. Poți numi variabila cum dorești și din acest motiv pe parcursul lucrării acesteia voi folosi și alte litere sau chiar cuvinte. Adu-ți mereu aminte că nu este musai ca variabila să se cheme `i` sau `x` sau cumva anume. Câtă vreme sunt respectate regulile la denumirea unei variabile, totul e ok. Se pune o singură literă pentru concizie.

În cazul în care se decide omiterea comparatorului, se va crea o buclă infinită, care poate fi întreruptă doar folosind comanda `break`.

```javascript
for (var x = 0; ;x++) {
  console.log(x);
  if (x > 5) { break }; // comparatorul
};
```

Pot fi omise toate cele trei expresii opționale, dar vor trebui tratate în blocul de execuție. Altfel, se intră într-o buclă infinită. Atenție, nu dorești acest lucru! Totul se oprește și de cele mai multe ori browserul se blochează. Fii foarte atent să pui condițiile de ieșire din buclă.

```javascript
console.time("start");
var x = 0;
for (;;) {
  console.log(x);
  // dacă nu introduci decizia
  // ai o buclă infinită
  if (x > 5) break;// comparatorul
  x++;// incrementorul
};
console.timeEnd("final");
```

Motivul pentru care bucla este una infinită este că blocul de condiție va fi evaluat la `undefined`, care este transformat într-un **falsey**, ceea ce conduce la execuția infinită. Adu-ți aminte că în JavaScript expresiile au un echivalent boolean.

## Prelucrarea datelor cu for

Să presupunem că avem nevoie să prelucrăm datele dintr-un array în care avem valori primitive. Nimic nu poate fi mai simplu: creăm o listă și apoi o parcurgem cu un enunț `for`, care permite prelucrarea unui array element cu element.

```javascript
var listă = [1, 2, 3];
for (var i = 0; i < listă.length; i++) {
  console.log(listă[i]);
};
```

După parcurgerea array-ului sunt returnate rezultatele. Dacă se mai dorește parcurgerea încă o dată, acest lucru nu este posibil cu excepția poziționării într-o funcție pe care o putem apela ori de câte ori dorim. Dacă am dori să avem acces la rezultatele de etapă, acest lucru nu este posibil. În exemplul de mai sus, am folosit utilitarul `console.log()` pentru prelucrare. Acesta nu ne ajută prea mult în afară de a vedea datele din array, în schimb, am putea introduce în exercițiul nostru o funcție pentru o prelucrare mult mai complexă fiecărei valori din array. Acest pas crește complexitatea exemplului nostru, dar și flexibilitatea în ceea ce privește multitudinea de prelucrări pe care le poți efectua.

Pentru a optimiza codul unei bucle efectuate pe un obiect **iterabil** este de preferat ca operațiunea de interogare a dimensiunii array-ului, în cazul în care acesta nu variază, să fie scoasă din evaluarea `for`. Facem acest lucru pentru că în cazul unei liste de câteva mii de repere, ar trebui ca motorul să calculeze de fiecare  dimensiunea array-ul. Aceasta este o operație inutilă.

```javascript
function prelucrează (elementArray) {
  return elementArray + 1;
};
let dimensiune = listă.length;
for (var i = 0; i < dimensiune; i++) {
  prelucrează(listă[i]);
}; // 4
```

Față de exemplul anterior, am avansat considerabil aplicând o funcție pe fiecare valoare din listă. Da, o funcție croită după necesitățile noastre. Câteva lucruri care încă persistă: trecerea se face din nou o singură dată și nu avem acces la valorile de etapă. Soluția pentru aceste cazuri este legată de modul în care declarăm variabilele în enunțul `for`.

Lucrul cu `for` pentru prelucrarea unei colecții de valori este caracterizat în literatura de specialitate ca fiind unul *imperativ*. Asta înseamnă că pentru fiecare element din colecție faci o evaluare ceea ce înseamnă evaluarea întregului cod din `for` pentru fiecare element.

```javascript
let colectie = [1, 2];
for (let x = 0; x < colectie.length; x++) {
  /*pentru fiecare colectie[x] fă ceva!*/
};
```

Pasul următor, așa cum am amintit mai sus, este să trecem la o abordare orientată pe utilizarea funcțiilor atunci când dorim să prelucrăm elementul colecției - o abordare funcțională, i-am spune. Dacă mă întrebi de ce, răspunsul este simplu. Imaginează-ți că în locul unei valori primare am avea un obiect care este o structură complexă. un obiect care este o fișă bibliografică din catalog. Dacă ai o colecție de fișe sau chiar întregul catalog pentru care dorești să modifici doar o singură informație comună dintr-un câmp, nu vei folosi niciodată o buclă `for`. Pentru că fiecare înregistrare este foarte complexă, vei opta pentru o funcție care să facă prelucrările necesare. Aici este punctul în care se deschide calea pentru utilizarea unor instrumente mai avansate precum `forEach()`, `map()`, `reduce()` sau `filter()`. Pssst! Dacă ești foarte curioasă, fă un salt la `forEach()` să vezi nițel rostul tuturor acestor pași ai înțelegerii în adâncime.

Pentru a te obișnui cu aceste instrumente mai avansate, ai nevoie să înțelegi bine funcțiile și exploatarea acestora sub formă de apeluri din alte funcții. Evident, este vorba despre callback-uri.

## Block-scoping în cazul buclelor

Subiectul constituirii mediului lexical în cazul buclelor se va dovedi imposibil de înțeles fără a le parcurge mai întâi pe cele dedicate mediului lexical, buclelor și funcțiilor. Hoistingul își face efectele și atunci când parcurgi structuri de date folosind instrucțiuni de iterare așa cum este `for`.

În cazul buclelor, ceea ce se întâmplă este că variabila folosită drept contor, este ridicată prin hoisting în mediul lexical gazdă. Efectul este incrementarea variabilei contor la finalul fiecărei iterații. Atenție, nu este memorată separat pentru fiecare iterare. Execuția lui `for` s-a încheiat fiind introdusă în mediul lexical nou redeclarata variabilă `x` care va avea ultima valoare rezultată în urma iterării.

```javascript

var x, y = [];
for(x = 0; x < 5; x++){
  console.log(x); // 0,1,2,3,4,5
  y.push(x);
};
console.log(x); // 5
console.log(y); // Array [ 0, 1, 2, 3, 4 ]
```

În cazul declarării contorului cu `let`:

```javascript
var y = [];
for(let x = 0; x < 5; x++){
  y.push(x);
};
console.log(x); // ReferenceError: x is not defined
console.log(y); // Array [ 0, 1, 2, 3, 4 ]
```

Pentru a exemplifica mai adânc vom încărca unui array cu funcții. Nu uita, o funcție este o valoare care poate fi pasată drept argument. Acest array va fi parcurs element cu element, adică funcție după funcție pentru a executa fiecare dintre ele. Se dorește obținerea unei serii de numere naturale.

```javascript
var apeluri = [];
for (var x = 0; x < 5; x++) {
  apeluri.push(function () {
    return x;
  });
};
console.log(apeluri.map(function(func){
  return func();
})); // Array [ 5, 5, 5, 5, 5 ]
```

Ceea ce s-a întâmplat este că înainte de a parcurge array-ul, variabila `x` a fost supusă deja mecanismului de *hoisting*, însemnând că este în scope-ul format de funcție, nu cel al lui `for`. Încărcând funcții în array, fiecare din ele face un closure (adică ține minte) pe valorile din mediul lexical din care au fost declarate. Rularea unei funcții din array sau pe toate la rând folosind `map`, va fi returnată valoarea ultimei iterații ale lui `for`, adică `5`. Pentru că variabila `x`, de fapt aparține mediului lexical global, prin mecanismul de shadowing, legătura a fost refăcută la fiecare iterație la o valoare nouă care a fost incrementată. Reține că `var` respectă doar mediul lexical al funcțiilor, altfel ajunge în global.

Folosind în locul lui `var` pe `let`, vom limita variabila la scope-ul blocului de cod în care a fost declarată, în cazul nostru a lui `for`. Adu-ți mereu aminte că `let` și `const` sunt **block scoped**.

```javascript
var apeluri = [];

for (let x = 0; x < 5; x++){
  apeluri.push(function(){
    return x;
  });
};

console.log(apeluri.map(function(callback){
  return callback();
})); // Array [ 0, 1, 2, 3, 4 ]
```

În cazul folosirii lui `let`, variabila va fi accesibilă la nivelul buclei, ceea ce înseamnă, de fapt că pentru fiecare iterație se va face un nou binding la câte o nouă variabilă `x` pentru fiecare dintre funcțiile încărcate în array. Fiecare variabilă nou creată va avea valoarea de la finalizarea iterației anterioare. Nu se va mai rescrie cu fiecare iterație valoarea lui `x`. Este valabil și pentru `for...in` și `for...of`.

```javascript
var apeluri = [],
    obi = {
      unu: 1,
      doi: 2
    };

for(let cheie in obi){
  // funcționează bine și cu const
  // pentru că modifici obiectul
  apeluri.push(function(){
    console.log(cheie);
  });
};

apeluri.forEach(function(functia){
  functia();
});
```

Înainte de ES6, care pune la dispoziție `let`, *fixarea* variabilei la valoarea iterației, se făcea printr-un IIFE (Immediately Invoked Function Expression):

```javascript
var apeluri = [];

for(var x = 0; x < 5; x++){
  apeluri.push((function(valoare){
      return function(){
        console.log(valoare);
      }
    }(x))); // x era conservat în mediul intern funcției
};

apeluri.forEach(function(callback){
  callback();
});
```

La fiecare iterare bucla creează o nouă variabilă și o inițializează cu valoarea variabilei cu același nume de identificator din iterarea precedentă.

### Salt și iterare cu verificare

În cazul în care este necesar, se poate face un `salt`, evitându-se execuția unuia din pașii buclei.

```javascript
for (var x = 0; x < 10; x++) {
  if (x === 5) {
    // daca nu verifici și tipul cu ===,
    // intri intr-o buclă infinită
    document.writeln(`am ajuns la ${x}`);
    continue;
  };
  console.log(x);
};
```

În exemplul prezentat am ajuns la `5`, care este afișat în pagina web prin utilizarea utilitarului `writeln` (*write line*, care înseamnă *scrie o linie*), pus la dispoziție de browser. Consola sare peste afișarea lui 5.

### Întreruperea execuției unei bucle

Uneori este nevoie ca atunci când o condiție internă buclei a fost atinsă, să oprim cu totul execuția buclei. Acest lucru se realizează cu `break`.

```javascript
for (let a = 0; a < 10; a++) {
  console.log(`bucla ${a}`);
  if (a > 0 && a % 3 === 0) {
    break;
  }
};
```

### Pași diferiți și variabili

Am văzut în exemple că pasul de incrementare a contorului este unu. Uneori ai nevoie ca pasul să fie diferit sau chiar variabil. Să presupunem că intervalul trebuie parcurs din 2 în 2.

```javascript
for (let a = 0; a < 10; a += 2) {
  console.log(`bucla ${a}`);
};
```

Poate vei avea nevoie ca incrementarea să se facă în funcție de o valoare externă care să dicteze câte iterații vei face.

```javascript
let variabil = 4;
for (let x = 0; x <= 20; x += variabil) {
  console.log(`bucla ${x}`);
};
```

### Bucle imbricate

Să presupunem că dorești ca atunci când parcurgi un interval, pentru fiecare iterație, să mai parcurgi un interval pentru care să faci niște operațiuni. Utilitatea se dovedește atunci când ai nevoie să construiești structuri de date, care conțin la rândul lor alte fragmente de date. Sună complicat, dar în simplitatea sa pentru o buclă într-o altă buclă, am putea rezuma ceea ce se petrece astfel: pentru fiecare iterație din bucla principală, se fac x iterații în bucla internă.

```javascript
for (let x = 0; x <= 5; x++) {
  console.log(`bucla principala: ${x}`);
  for (let y = 0; y <= 2; y++) {
    console.log(`bucla internă: ${y}`);
  };
};
```

Utilitatea buclelor în alte bucle este pentru a crea array-uri multidimensionale, de exemplu. Și pentru că am menționat array-urile, structuri de date pe care încă nu le-am abordat structurat, în *manipularea* datelor conținute de acestea, `for` constituie un instrument de bază. Mai mult, `for` este adeseori folosit pentru a **împinge** date într-un array. La fiecare iterație este *alimentat* un array folosind metoda *push* cu rezultatul evaluării codului.

```javascript
let lista = [];
for (let x = 0; x <= 3; x++) {
  // alimentez array-ul la fiecare iterație
  lista.push(x);
};
console.log(lista); // Array [ 0, 1, 2, 3 ]
console.log(lista.length); // 4
```

Un singur amănunt mai adaug la informațiile despre array-uri. În orice moment se poate afla dimensiunea unui array, dacă se apelează proprietatea `length`. În cazul exemplului nostru, lungimea este `4`, adică are patru elemente. Este chiar intervalul închis \[0, 3].

### Enunțul for poate fi folosit și în lucrul cu șirurile de caractere

Șirurile de caractere au caracteristici asemănătoare unui array. Deci, au proprietate care indică dimensiunea șirului de caractere.

Putem avea cazul în care la un caracter poți adăuga un altul până când numărul lor va atinge limita specificată prin valoarea lui `length`.

```javascript
for (var i = "»"; i.length < 5; i += "~") {
  console.log(i);
};
/*
»
»~
»~~
»~~~
 */
```

În exemplul nostru, facem o adăugare a unui caracter la unul definit inițial.

### Lucrul cu Document Object Model - DOM

Buclele cu `for` pot fi folosite pentru introducerea de elemente în DOM.

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="utf-8">
    <title>Introducerea de elemente cu for</title>
  </head>
  <body>
    <h1>Introducere elemente în DOM folosind iterarea</h1>
    <div class="" id="carlig"></div>
  </body>
  <script>
    var x, y;
    console.time("start");
    for (x = 0; x < 20; x++) {
      y = document.createElement('p');
      y.innerText = x;
      document.body.appentChils(y);
    };
    console.timeEnd("final");
  </script>
</html>
```

## Folosirea lui for cu variabile multiple

În enunțurile `for` se pot introduce mai multe variabile. Un exemplu pentru a căuta membrii șirului lui Fibonacci implică declararea mai multor variabile inițiale. După aceea, în expresia de incrementare sunt manipulate pentru a avansa.

```javascript
for(let temp, i = 0, j = 1; j < 4; temp = i, i = j, j = i + temp) {
  console.log(j);
};
```

![Ilustrație pentru ciclurile for](for-ilustratie-for-fibonacci.png)

Pentru că aceeași problemă se poate rezolva folosindu-ne de recursivitatea funcțiilor, vom introduce aici soluția pentru a avea o ancoră către subiectul recursivității, când vom aprofunda funcțiile.

```javascript
function fibonacci (x) {
  if (x < 2) {
    return x
  }
  return fibonacci (x - 1) + fibonacci (n - 2)
};
```

## Carte de bucate

### Inversarea unui șir de caractere

Uneori ai nevoie de inversarea unui șir de caractere. Poți face acest lucru folosind o buclă `for` cu ajutorul căreia parcurgi caracter cu caracter. Pe fiecare dintre acestea le adaugi unui nou șir format ce va conține la final varianta inversată.

```javascript
let șir = 'ceva', șirInversat = '';
for (let i = 0; i < șir.length; i++) {
  șirInversat = șir[i] + șirInversat;
}
console.log(șirInversat); // avec
```

Folosind `for...of` sintaxa se reduce semnificativ, fiind eliminate posibilele erori de redactare. Adu-ți mereu aminte de faptul că iterările cu `for...of` sunt o specializare a lui `for` în scopul parcurgerii unor structuri de date, precum `Array`, `Map` și `Set`.

```javascript
let șir = 'ceva', șirInversat = '';
for (let i of șir) {
  șirInversat = i + șirInversat;
}
```

Și acum pentru a înțelege că există posibilitatea de a face aceste operațiuni și cu instrumentele pe care le avem în vizor spre finalul acestui manual, voi adăuga și posibilitatea de a prelucra șirul nostru de caractere folosind `Array.prototype.reduce()`.

```javascript
let șir = 'ceva', șirInversat = '';
șirInversat = șir.split('').reduce((acumulator, curent) => {
  return curent + acumulator;
}, '');
console.log(șirInversat);
```

Și ca să folosim toate trucurile moderne ale ES6 (fat arrows și ASI), vom putea condensa expresia funcției callback pasată lui reduce și mai mult, ajungând la următoarea formulare:

```javascript
let șir = 'ceva', șirInversat = '';
șirInversat = șir.split('').reduce((acumulator, curent) => curent + acumulator, '');
console.log(șirInversat);
```

## Mantre

-   toate expresiile din blocul de inițializare pot lipsi, dar trebuie să existe terminatoarele punct și virgulă.

## Resurse

-   Ethan Brown. Learning JavaScript
-   [Interval (mathematics), Wikipedia](https://en.wikipedia.org/wiki/Interval_(mathematics))
-   [Edsger W. Dijkstra](https://en.wikipedia.org/wiki/Edsger_W._Dijkstra)
