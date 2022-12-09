
Încercați să îl rulați:

```cod js 
let str = "Buna";

str.test = 5; // (*)

alert(str.test);
```

În funcție de faptul că aveți „utilizare strictă” sau nu, rezultatul poate fi:
1. `nedefinit` (fără mod strict)
2. O eroare (mod strict).

De ce? Să reluăm ceea ce se întâmplă la rândul „(*)”:

1. Când o proprietate a lui `str` este accesată, este creat un „obiect wrapper”.
2. În modul strict, scrierea în el este o eroare.
3. În caz contrar, se continuă operația cu proprietatea, obiectul primește proprietatea `test`, dar după aceea "obiectul wrapper" dispare, deci în ultima linie `str` nu are nicio urmă a proprietății.

**Acest exemplu arată clar că primitivele nu sunt obiecte.**

Nu pot stoca date suplimentare.
