# Evaluarea

Am introdus capitolul care prezintă valorile de lucru pentru că aceste valori sunt **operanzii** care întră în combinație cu operatorii. Aceste expresii exprimă dorința de a ajunge la un rezultat în urma evaluării. Când vrem să adunăm două valori, folosim caracterul plus pentru a indica evaluatorului (motorul limbajului) că dorim să ajungem la valoarea cumulată.
La un moment dat, vei dori rezultatul evaluării unor expresii de o mare complexitate. Acum este necesar să înțelegem cât de important este să privim expresiile prin lupa evaluării. Ochiul antrenat le va detecta parcurgându-le mental, înțelegând ce fac toți operatorii angrenați.

**Operanzii sunt expresii**.

Operatorii sunt **semne grafice** sau **cuvinte cheie** care indică ce operațiune se va efectua la momentul evaluării expresiei. Aceste semne grafice sunt semnele operațiunilor matematice, adunare, scădere, compararea valorilor și așa mai departe.

Să ne amintim că expresiile pot fi constituite pur și simplu din declararea unei valori sau a unei variabile, dar și din înșiruirea de operanzi și operatori. În unele lucrări dedicate în general programării veți mai întâlni opinia că operanzii pot fi percepuți drept substantive, iar operatorii ca adevărate verbe.

**Moment ZEN**: Un program JavaScript este evaluarea unui set de expresii, care pentru a fi *rezolvate*, mai întâi trebuie să rezolvi din aproape în aproape toate celelalte expresii mai mici.

În programare există două mari categorii de operatori: operatorii unari și cei binari. Operatorii unari sunt acei operatori care se aplică unui singur operand. Operatorii binari sunt cei care implică doi operatori. Ca și în cazul matematicii, operatorii au o anumită ordine, o anumită întâietate la evaluare a unora față de alții. Ne aducem aminte de la aritmetică că înmulțirea se face înaintea adunării și a scăderii.
Până acum v-am obișnuit cu unul care este indispensabil, cel care atribuire a valorilor `=` (semnul egal). Este operatorul care pur și simplu face legătura dintre valoare și numele sub care poate fi regăsită. Haideți să pornim încetișor să vedem despre ce este vorba și pentru asta vom reveni la cele mai simple concepte ale operațiunilor matematice. Da, știu. Mate! Da' promit că nu doare. Hai să vedem care-i treaba cu asociativitatea.

## Asociativitatea operatorilor

Este o proprietate care indică ordinea în care sunt procesați operatorii de același rang.

```javascript
1 + 2 + 3
```

Asociativitate stângă este atunci când grupezi termenii din partea stângă.

```javascript
(1 + 2) + 3
```

Asociativitatea dreaptă este atunci când poți grupa termenii de la dreapta.

```javascript
1 + (2 + 3)
```

Asociativitatea dreaptă funcționează și pentru următorul exemplu.

```javascript
x = y = 1;
```

Valoarea `1` este atribuită lui `y`, iar `y` este atribuit lui `x`.

## Truthy și falsey

Javascript operează cu diferite tipuri de valori, dar toate acestea sunt evaluate de către motorul JavaScript pentru a le reduce la un corespondent boolean, adică dacă pot fi reduse la `true` și sunt *truthy* (adevărate) sau la `false`, numite *falsey* (falsități).

Valorile pe care JavaScript le consideră a fi în categoria falsităților (*falsey*) sunt: `false`, `0`, `''` (un șir de caractere vid), `NaN` (Not-a-Number), `undefined` și `null`. Orice altceva este considerat a fi *truthy*. Pe parcursul acestei lucrări vom folosi denumirile în limba engleză.

Funcțional vorbind, operatorii se pot împărți în două categorii: operatorii unari în sensul că-și produc efectele asupra unui singur operand și cei binari care-și produc efectele la momentul evaluării asupra a doi operanzi. În afara acestei categorisiri mai sunt și alți operatori care ar putea fi grupați după sarcina pe care o au și așa mai departe.

Pentru a înțelege pe deplin operatorii, trebuie să ne întoarcem la ceea ce înseamnă expresiile și cum arată acestea. Ceea ce este util să ne aducem aminte este faptul că într-un enunț format dintr-o singură expresie sau în cazul unei expresii, care face parte dintr-un enunț format din mai multe, avem două zone importante:

-   partea din stânga a operatorului (în engleză *Left Hand Side* - LHS) și
-   partea din dreapta a operatorului (în engleză *Right Hand Side* - RHS).

Adu-ți mereu aminte că operatorii stabilesc o relație între operandul (o expresie) din stânga sa cu operandul (o expresie) din dreapta sa. La momentul evaluării, operandul mai întâi încearcă să **transforme** valorile în tipul de care are nevoie, dacă în expresie sunt prezente alte valori decât cele așteptate.

Această operațiune se numește în engleză **coercion**, care l-am putea traduce în contextul nostru ca și „constrângere”. În fapt, se reduce la încercarea de a transforma o valoare de un anumit tip într-un tip ce ar permite o evaluare a expresiei în care este prezent un anumit operator.

## Resurse

[JSFuck](http://www.jsfuck.com/)
