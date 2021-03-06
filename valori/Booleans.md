# Valorile boolean

Numele acestor valori ne aduce aminte de George Boole, cercetătorul care a oferit o variantă algebrică de calcul al unor astfel de valori. Această valoare este o primitivă.

Acestea sunt `true` și `false`.

Testarea după aceste valori este foarte importantă în logica unui program. În funcție de valoare sunt luate decizii în ceea ce privește firul de execuție.

Reține faptul că toate valorile la care ajungi în urma evaluării expresiilor JavaScript au un corespondent boolean după care poți face o verificare, investigând dacă se reduce la adevăr (*truthy*) sau fals (*falsey*). Poți chiar să testezi apelând obiectul intern căruia îi pasezi drept parametru valoarea de test.

```javascript
Boolean('test'); // true
```

Valorile care sunt evaluate la `false`:

-   `""` (un șir de caractere vid marcat prin ghilimele duble),
-   `''` (un șir de caractere vid marcat prin ghilimele simple),
-   `0`,
-   `NaN`,
-   `false`,
-   `null`,
-   `undefined`
