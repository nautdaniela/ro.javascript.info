# Metode ale primitivelor

JavaScript ne permite să lucrăm cu primitive (șiruri, numere etc.) ca și cum ar fi obiecte. Ele oferă, de asemenea, metode de apel ca atare. Le vom studia în curând, dar mai întâi vom vedea cum funcționează pentru că, desigur, primitivele nu sunt obiecte (și aici vom face și mai clar).

Să ne uităm la distincțiile cheie dintre primitive și obiecte.

Un primitiv

- Este o valoare de tip primitiv.
- Există 7 tipuri primitive: `șir`, `număr`, `bigint`, `boolean`, `simbol`, `null` și `nedefined`.

Un obiect

- Este capabil să stocheze mai multe valori ca proprietăți.
- Poate fi creat cu `{}`, de exemplu: `{nume: "Ioan", vârsta: 30}`. Există și alte tipuri de obiecte în JavaScript: funcțiile, de exemplu, sunt obiecte.

Unul dintre cele mai bune lucruri despre obiecte este că putem stoca o funcție ca una dintre proprietățile sale.

```cod js 
let john = {
  name: "Ioan",
  sayHi: function() {
    alert("Buna amice!");
  }
};

john.sayHi(); // Buna amice!
```

Deci aici am creat un obiect `john` cu metoda `sayHi`.

Multe obiecte încorporate există deja, cum ar fi cele care lucrează cu date, erori, elemente HTML etc. Au proprietăți și metode diferite.

Dar, aceste caracteristici vin cu un cost!

Obiectele sunt „mai grele” decât primitivele. Acestea necesită resurse suplimentare pentru a susține echipamentul intern.

## Un primitiv ca obiect

Iată paradoxul cu care se confruntă creatorul JavaScript:

- Există multe lucruri pe care ar dori să le faci cu o primitivă, cum ar fi un șir sau un număr. Ar fi grozav să le accesați folosind metode.
- Primitivele trebuie să fie cât mai rapide și ușoare.

Soluția pare puțin incomodă, dar iată-o:

1. Primitivele sunt încă primitive. O singură valoare, după dorință.
2. Limbajul permite accesul la metode și proprietăți ale șirurilor de caractere, numerelor, booleanelor și simbolurilor.
3. Pentru ca acest lucru să funcționeze, este creat un „înveliș de obiect” special care oferă funcționalitatea suplimentară și apoi este distrus.

„Învelișurile de obiecte” sunt diferite pentru fiecare tip primitiv și se numesc: `String`, `Number`, `Boolean`, `Symbol` și `BigInt`. Astfel, ele oferă seturi diferite de metode.

De exemplu, există o metodă de șir [str.toUpperCase()](https://developer.mozilla.org/en/docs/Web/JavaScript/Reference/Global_Objects/String/toUpperCase) care returnează un `str` cu majuscule.

Iată cum funcționează:

```cod js 
let str = "Buna";

alert( str.toUpperCase() ); // BUNA
```

Simplu, nu? Iată ce se întâmplă de fapt în `str.toUpperCase()`:

1. Șirul `str` este o primitivă. Deci, în momentul accesării proprietății sale, este creat un obiect special care cunoaște valoarea șirului și are metode utile, precum `toUpperCase()`.
2. Metoda respectivă rulează și returnează un șir nou (afișat de `alert`).
3. Obiectul special este distrus, lăsând în pace `str` primitiv.

Deci primitivii pot oferi metode, dar rămân totuși ușoare.

Motorul JavaScript optimizează foarte mult acest proces. Poate chiar sări peste crearea obiectului suplimentar. Dar trebuie să respecte specificațiile și să se comporte ca și cum ar crea una.

Un număr are metode proprii, de exemplu, [toFixed(n)](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Number/toFixed) rotunjește numărul la precizia dată:

```cod js 
let n = 1.23456;

alert( n.toFixed(2) ); // 1.23
```

Vom vedea metode mai specifice în capitolele <informatii:numbere> și <informatii:siruri>.

````warn header="Constructorii `String/Number/Boolean` sunt numai pentru uz intern"
Unele limbaje precum Java ne permit să creăm în mod explicit „obiecte wrapper” pentru primitive folosind o sintaxă precum `new Number(1)` sau `new Boolean(false)`.

În JavaScript, acest lucru este posibil și din motive istorice, dar foarte **nerecomandat**. Lucrurile vor înnebuni în mai multe locuri.

De exemplu:
```cod js
alert( typeof 0 ); // "numar"

alert( typeof new Number(0) ); // "obiect"!
```

Obiectele sunt întotdeauna adevărate în „if”, așa că aici va apărea alerta:

```cod js 
let zero = new Number(0);

if (zero) { // zero este adevărat, pentru că este un obiect
  alert( "zero este adevărat!?!" );
}
```

Pe de altă parte, folosirea acelorași funcții `String/Number/Boolean` fără `new` este un lucru total sănătos și util. Ele convertesc o valoare în tipul corespunzător: într-un șir, un număr sau un boolean (primitiv).

De exemplu, acest lucru este pe deplin valabil:
```js
let num = Number("123"); // converti un șir în număr
```
````


````warn header="null/undefined nu au metode"
Primitivele speciale `null` și `undefined` sunt excepții. Nu au „obiecte wrapper” corespunzătoare și nu oferă metode. Într-un fel, ei sunt „cei mai primitivi”.

O încercare de a accesa o proprietate de asemenea valoare ar da eroarea:

```js run
alert(null.test); // eroare
````

## Rezumat

- Primitivele cu excepția „null” și „undefined” oferă multe metode utile. Le vom studia în capitolele următoare.
- În mod formal, aceste metode funcționează prin intermediul obiectelor temporare, dar motoarele JavaScript sunt bine reglate pentru a optimiza acest lucru în interior, deci nu sunt costisitoare de apelat.
