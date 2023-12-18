# Linked list

Aici voi nota informatii generale legate de structura de date numita Linked list.

## Ce este un Linked list?

Un linked list este o structura de date liniara similara cu arrays. Este o colectie de **noduri** care sunt legate intre ele.

### Ce este un nod?

Un nod reprezinta o componenta fundamentala a linked list. Acesta contine doua componente principale:

1. Valoarea(data) -> Aceasta reprezinta informatia sau datele pe care nodul le sctocheaza. Poate fi orice tip de date cum ar fi `int`, `str`, sau o structura de date mai complexa cum ar fi alte liste, dictionare etc.

2. Referinta(Link) -> Acesta este un pointer sau o referinta(legatura) catre urmatorul nod din lista. In linked list fiecare nod contine doar o singura referinta catre urmatorul nod, iar intr-un double linked list un nod ar contine doua referinte una pentru urmatorul nod si alta pentru nodul precedent.

Exemplu de linked list (arhitectura):

![linked list](https://media.geeksforgeeks.org/wp-content/uploads/20230503102657/LLdrawio.png)


Acesta este felul cum un linked list simplu functioneaza. `Head` reprezinta primul nod din linked list si locul de unde se porneste. Incepand de la `Head` putem traversa lista prin legaturile dintre noduri. 


Exemplu de double linked list:

![Double linked list](https://media.geeksforgeeks.org/wp-content/cdn-uploads/gq/2014/03/DLL1.png)

Felul cum un double linked list functioneaza este similar cu a unei linked list simpla. Se porneste de la `head` si se parcurge lista pana cand ultimul element are pointerul spre null. Apoi putem parcurge invers lista incepand de la ultimul element pana la primul element care are pointerul spre null.

## De ce linked list?

Linked list sunt folosite în diverse domenii ale programării datorită caracteristicilor lor specifice. Iată câteva utilizări comune pentru listele înlănțuite:

1. **Alocare dinamică a memoriei**: Linked list permit alocarea dinamică a memoriei pentru elementele lor, ceea ce le face flexibile în gestionarea resurselor.

2. **Inserare și ștergere eficientă**: Adăugarea sau eliminarea unui element într-o listă înlănțuită poate fi realizată eficient, în comparație cu un array, deoarece nu este necesar să realocăm sau să mutăm elementele adiacente.

3. **Stocarea datelor variabile**: Linked list se adaptează ușor la modificări ale dimensiunii datelor, ceea ce le face utile în situații în care dimensiunea sau structura datelor poate varia dinamic.

4. **Implementarea altor structuri de date**: Linked list sunt utilizate pentru implementarea altor structuri de date, cum ar fi **queues** și **stacks**.

5. **Manipularea datelor în timp real**: Linked list pot fi utile în aplicații care implică manipularea continuă și dinamică a datelor în timp real, cum ar fi în jocuri sau aplicații grafice.

6. **Implementarea algoritmilor**: Anumite algoritmi beneficiază de utilizarea listelor înlănțuite pentru a simplifica și accelera operațiile de inserare sau ștergere.

7. **Graful listelor înlănțuite**: Linked list pot fi utilizate pentru a implementa structuri de date mai complexe, cum ar fi graphs, în care nodurile pot fi conectate într-un mod neconvențional.

În general, linked lists oferă o flexibilitate și eficiență în gestionarea datelor dinamice și sunt alese în funcție de cerințele specifice ale unei aplicații sau algoritmi.