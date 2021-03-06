# Iterații

Partea cea mai valoroasă a programării este aceea că poți lua un set de date pe care le poți parcurge element cu element, aplicând transformări sau căutări după anumite criterii, cu scopul de a obține un anumit rezultat dorit. Este ceea ce se poate înțelege prin **ciclu**, adică o mișcare repetitivă sau aplicarea repetată a unor proceduri pe elementele individuale ale unei colecții. De altfel, în practica de zi cu zi, veți auzi interșanjabil termenii de buclă, iterare și uneori ciclare.

Dicționarul explicativ ne dă o definiție foarte utilă pentru iterare: *repetare a unui anumit procedeu de calcul, prin aplicarea lui la rezultatul calculului din etapa precedentă*.

## Bucle

Buclele sunt cel mai la îndemână instrument de a parcurge un set de date.
Folosirea buclelor presupune utilizarea repetată a unei secvențe de instrucțiuni. Îi mai spunem **ciclare** sau **iterare**. În fapt, ceea ce se întâmplă este o repetarea ritmică a unui set de instrucțiuni. Fiecare rezultat al fiecărei iterații este supus verificărilor.
Alternativa la procesele repetitive, la ciclurile iterative realizate cu buclele este **recursivitatea**. Recursivitatea nu implică conceptul de ciclu, ci acela de apel repetat al unei funcții din interiorul său.

## Protocoale de iterare

Am menționat deja despre protocoalele de iterare. ECMAScript 2015 (ES6) a introdus un nou mecanism de parcurgere a datelor numit **iterare**. Mai exact, un **protocol de iterare** pentru că iterarea acest concept este în ADN-ul programării.

În anul 1994, patru specialiști în informatică căutau să unifice soluțiile folosite în practica programării computerelor în șabloane ușor de înțeles. Cei patru, Erich Gamma, Richard Helm, Ralph Johnson și John Vlissides, numiți de comunitate *Gang of Four*, investighează în lucrarea *Design Patterns: Elements of Reusable Object-Oriented Software* mai multe soluții uniformizate la nivel abstract prin ceea ce se numește *design patterns*. Unul dintre acestea se numește *Iterator*, fiind catalogat un model comportamental. Intenția acestui model de organizare a funcționalităților era de a:

> oferi o cale pentru a accesa secvențial elementele unui obiect agregat fără a expune reprezentarea sa internă.

Este menționat faptul că acestui șablon i se mai spune și *Cursor* și cea mai importantă mențiune este legată de domeniul de aplicare. Astfel, un șablon Iterator este construit pentru *a oferi o interfață uniformă folosită în traversarea diferitelor structuri de agregare*. Trebuie adăugat faptul că iterarea se poate face doar pe structuri sincrone așa cum sunt array-urile. Nu se pot aplica în cazul evenimentelor, care sunt asincrone în natură.

### Cum se face iterarea

Pentru a lămuri aspectele privind iterarea, vom recurge din nou la explicațiile *GoF*, care spun că iterarea este un algoritm de parcurgere (în engleză *traversal*) a unei structuri de date care folosește un *cursor* a cărui sarcină este să țină minte unde a ajuns (să memoreze starea). Dacă acest cursor este acționat cu o comandă `next`, își va modifica starea imediat ce va fi parcurs încă un element al structurii de date.

În parcurgerea unui set de date, atunci când rezultatul unui pas devine valoarea de start pentru următorul, atunci vorbim despre iterare. În acest moment avem două concepte centrale care merită atenția noastră deplină:

-   **iterable** fiind structura de date care expune elementele pentru a fi accesate public. Face acest lucru implementând o metodă care returnează un obiect numit *iterator*. Această metodă nu este abstractă, ci poate fi apelată în obiectele care pot fi iterate (`[Symbol.iterator]()`),
-   **iterator** fiind, de fapt, un pointer (în limba română ar fi tradus ca *indicator* sau *cursor*, dar poți să ți-l închipui ca un semn de carte) pentru traversarea elementelor unei structuri de date.

### Când apare

-   `for...of`,
-   `Array.from()`,
-   operatorul spread (`...`),
-   constructorul pentru Map `new Map([['varza',1],[2, true]])`,
-   constructorul pentru Set `new Set([1,'doi',false])`,
-   `Promise.all()` și `Promise.race()`,
-   `yield* unObiectIterabil`.

Există două protocoale (convenții aplicate unitar pentru iterări):

-   Iterable protocol - protocolul aplicat unei structuri de date care este iterabilă și
-   Iterator protocol - protocolul de iterare, care se va aplica acelei structuri de date.

## Iterable

Acest protocol permite obiectelor să-și definească sau să-și particularizeze comportamentul la momentul iterării, adică ce valori vor fi generate cu un enunț `for...of`.

Bucla `for...of` poate itera prin următoarele obiecte care respectă **protocolul iterator**: `Array`, `Map`, `Set`, `String`, `TypedArray` și `arguments`.

Pentru a fi iterabil, un obiect trebuie să aibă implementată la nivelul obiectului intern de la care moștenește metoda `@@iterator`. Acest lucru înseamnă că obiectul (sau unul din obiectele din lanțul prototipal), trebuie să aibă o proprietate cu o cheie `[Symbol.iterator]`. Valoarea sa este o funcție fără argumente ce returnează un obiect. Acest obiect returnat se conformează protocolului de interare (**iterator protocol**), ceea ce îl face pretabil unei prelucrări cu `for...of`, de exemplu.

Să luăm un exemplu care se bazează pe moștenirea de la obiectul intern `String` prin ambalare. Acest obiect intern este un exemplu de obiect iterabil construit în limbaj.

```javascript
let unSir = "un sir de caractere";
typeof unSir[Symbol.iterator]; // "function"
```

De fapt, această metodă este o fabrică (un șablon de programare numit în domeniu: **factory**) pentru iteratori. Ori de câte ori un obiect trebuie să fie iterat, este invocată metoda `@@iterator` fără nici un argument. Este creat și returnat un obiect iterabil. Folosind metoda `next()` obții un obiect care are propritățile `value` și `done`. Cheia `value` are valoarea elementului la care a ajuns *cursorul* în parcurgerea obiectului iterabil, iar `done` prin valoarea boolean confirmă parcurgerea integrală a obiectului iterabil.

```javascript
let iterator = [1, 2, 3][Symbol.iterator](),
    element;
while( !(element = iterator.next()).done ) {
  console.log(element.value);
};
```

**Moment Zen**: Șirurile de caractere și seturile de valori sunt structuri iterabile.

Odată cu ECMAScript 2015, beneficiem de enunțul `for...of`, care va face exact ce am realizat mai sus generând obiectul iterator. Array-urile sunt obiecte care implementează protocolul de iterare.

```javascript
for(let x of [1, 2, 3]){
  console.log(x);
};
```

Parcurgerea se face automat, rezultatele fiind oferite la încheierea iterării. Ce te faci în momentul în care dorești să ai acces secvențial la valorile unei colecții? În acest caz, vom apela la funcțiile generator.

## Iterator

Definește o modalitate standard pentru a produce o secvență de valori finite sau infinite. Se comportă ca un pointer.

**Moment Zen**: Un obiect este un iterator atunci când implementează metoda `next()`.

Metoda `next()` este o funcție care nu primește argumente, dar care returnează un obiect cu două proprietăți:

-   `done` care este un `Boolean` cu cele două alternative: dacă `true`, atunci iteratorul a trecut de finalul secvenței pe care a avut-o de parcurs; dacă `false` înseamnă că a produs următoarea valoare din secvență;
-   `value` care este valoarea returnată de iterator. Se poate omite atunci când `done` este `true`.

Aceste protocoale implementate cu ajutorul simbolurilor, permit parcurgerea și prelucrarea datelor care au fost introduse în valori ce moștenesc automat de la tipurile de obiecte interne corespondente. La ce mă refer este faptul că indiferent de natura datelor, text sau un array, ori un obiect *dicționar*, vor fi *ambalate* automat în obiectul intern corespondent. Acesta este și motivul pentru care poți aplica metode ale obiectelor interne direct pe valoarea identificată de o variabilă.

Dacă este nevoie, poți converti un obiect simplu în unul iterabil. Tot ce trebuie să faci este să adaugi o metodă `[Symbol.iterator]` pentru a adăuga protocolul de iterare.

```javascript
let colectie = [11, 22, 33]; // este obiectul
class Transformat {
  constructor (colectie) {
    this.colectie = colectie;
    this.idx = 0;
  }

  [Symbol.iterator] () {
    return this;
  }

  next () {
    if (this.idx <= this.colectie.length) {
      let obi = {value: colectie[this.idx], done: false};
      this.idx++;
      return obi;
    }
    return {value: undefined, done: true}
  }
}

let iterator = new Transformat(colectie);
iterator.next();
```

După cum se observă, am generat un obiect în baza unei clase, care prelucrează o colecție. Exemplul folosește un array care este un obiect. Acesta deja implementează protocolul iterator, dar am făcut acest exercițiu pentru a ilustra mecanismul intern al unui iterator. La nevoie poți transforma un obiect obișnuit creat printr-o expresie literală într-un iterator.

```javascript
function scotNr () {
  let nr = Math.random() * 10;
  return nr;
};

const obiect = {
  // un factory de iteratoare
  [Symbol.iterator]: () => {
    return {
      next: () => {
        let numar = scotNr() > 3;
        if(!numar) {
          return {
            value: scotNr(),
            done: false
          }
        }
        return { done: true }
      }
    }
  }
}
for (let rezultat of obiect) {
  console.log(rezultat);
};
```

Pentru a înțelege că generatoarele sunt doar un adaos sintactic pentru iteratoare, putem reformula factory-ul de iteratoare într-un generator.

```javascript
function scotNr () {
  let nr = Math.random() * 10;
  return nr;
};
const obiect = {
  // un factory de iteratorare
  [Symbol.iterator]: function* () {
    while(true) {
      let numar = scotNr() > 3;
      if(numar) {
        return;
      }
      yield scotNr();
    }
  }
}
for (let rezultat of obiect) {
  console.log(rezultat);
};
```

## Avantaj

Poți construi obiecte iterator care să genereze la infinit un anumit rezultat pentru că `done` nu va fi niciodată `false`.

```javascript
class UnGenerator {
  [Symbol.iterator](){
    return this;
  }
  next () {
    return {
      value: Math.random(),
      done: false
    };
  }
}

let obi = new UnGenerator(),
    contor = 0;

for (let valoare of obi) {
  console.log(valoare.toFixed(4));
  if (5 == ++contor) {
    break;
  }
};
```

Iteratorul a fost întrerupt brusc și o reutilizare ar conduce la rezultate neașteptate. Pentru a preveni acest lucru, se va implementa o metodă care va seta `done` la `true`.

```javascript
class UnGenerator {
  [Symbol.iterator](){
    return this;
  }
  next () {
    if (this.done) {
      return {value: undefined, done: true}
    }
    return {value: Math.random(), done: this.done}
  }
  return () {
    this.done = true;
    return {done: true}
  }
}
```

## Enunțul while

În engleză *while* se traduce în limba română prin `câtă vreme`. Verbalizarea acestei comenzi ar fi *de câte ori evaluarea expresiei conduce la o valoare ce poate fi redusă la un boolean `true`, execută codul dintre acolade*.

```javascript
var x = 0;
while (x < 10) {
  console.log(x); // execută funcția log
  x++;            // modifică valoarea
};
```

Remarcă faptul că testul condiției se face la începutul fiecărei iterații. Acest lucru înseamnă că în caz de valoare `false`, codul nu se va executa nici măcar pentru o singură iterație.

While își are locul său, dar practica înclină către folosirea instrucțiunii `for`, care în condiția de test permite introducerea a trei expresii. Evaluarea acestor trei expresii va determina continuarea iterării sau nu.

Folosește `while` acolo unde condiția de test este simplă.

Când vorbim de simplă nu înseamnă să te limitezi la o singură expresie, ci poți avea una care să fie o combinație destul de elaborată ca și condiție.

```javascript
var a = 5, b = 4;
while (a < 10 && b > 3) {
  console.log(a);
  a++; b++;
};
```
-   `value` care este valoarea returnată de Iterator. Se poate omite atunci când `done` este `true`.

## Resurse

-   [MDN - Iteration protocols](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Iteration_protocols)
-   [Iterables and iterators](http://exploringjs.com/es6/ch_iteration.html)
-   [Design Patterns](https://en.wikipedia.org/wiki/Design_Patterns)
