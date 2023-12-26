# Sortarea elementelor 

### Sortarea este definită ca o aranjare a datelor într-o anumită ordine.

Tehnicile de sortare sunt folosite pentru a aranja datele (în mare parte numerice) într-o ordine crescătoare sau descrescătoare. Este o metodă folosită pentru reprezentarea datelor într-un format mai inteligibil. Este un domeniu important al informaticii. Sortarea unei cantități mari de date poate necesita o cantitate substanțială de resurse de calcul dacă metodele pe care le folosim pentru sortarea datelor sunt ineficiente. Eficiența algoritmului este proporțională cu numărul de elemente pe care le parcurge. Pentru o cantitate mică de date, o metodă complexă de sortare poate crea mai multe probleme de ineficienta.

Pe de altă parte, pentru cantități mai mari de date, dorim să creștem eficiența și viteza pe cât posibil. Vom discuta acum mai multe tehnici de sortare și le vom compara în funcție de complexitatea lor în timp.

![Exemplu sortare](https://media.geeksforgeeks.org/wp-content/uploads/20210812115830/sortexample.jpg)

Unele dintre exemplele reale de sortare sunt:

1. **Director telefonic**: este o carte care conține numerele de telefon și adresele persoanelor în ordine alfabetică.
2. **Dicționar**: este o colecție imensă de cuvinte împreună cu semnificațiile lor în ordine alfabetică.
3. **Lista de contacte**: este o listă de numere de contact ale persoanelor în ordine alfabetică de pe un telefon mobil.

Înainte de a discuta despre diferiții algoritmi utilizați pentru sortarea datelor care ni se oferă, ar trebui să ne gândim la operațiunile care pot fi utilizate pentru analiza unui proces de sortare. În primul rând, trebuie să comparăm valorile pentru a vedea care dintre ele este mai mică și care este mai mare, astfel încât să poată fi sortate într-o ordine, va fi necesar să avem o modalitate organizată de a compara valorile pentru a vedea că dacă sunt în ordine.

### Diferitele tipuri de comenzi sunt:

1. **Ordine crescătoare**: Se spune că un set de valori este în ordine crescătoare atunci când fiecare element succesiv este mai mare decât elementul său anterior. De exemplu: 1, 2, 3, 4, 5. Aici, succesiunea dată este în ordine crescătoare.
2. **Ordine descrescătoare**: Se spune că un set de valori este în ordine descrescătoare atunci când elementul succesiv este întotdeauna mai mic decât cel anterior. De exemplu: 5, 4, 3, 2, 1. Aici succesiunea dată este în ordine descrescătoare.
3. **Ordine non-crescătoare**: Se spune că un set de valori este în ordine necrescătoare dacă fiecare element prezent în secvență este mai mare sau egal cu (i-1)-lea element. Această ordine apare ori de câte ori există numere care se repetă. De exemplu: 1, 2, 2, 3, 4, 5. Aici 2 se repetă de două ori.
4. **Ordine non-descrescătoare**: Se spune că un set de valori este în ordine nedescrescătoare dacă fiecare element prezent în secvență este mai mic sau egal cu (i-1)-lea element. Această ordine apare ori de câte ori există numere care se repetă. De exemplu: 5, 4, 3, 2, 2, 1. Aici 2 se repetă de două ori.

## Tehnici de sortare

Diferitele implementări ale tehnicilor de sortare în Python sunt:

1. Bubble Sort
2. Selection Sort
3. Insertion Sort

Vom discuta separat pentru fiecare algoritm pentru a intelege totul foarte bine.

