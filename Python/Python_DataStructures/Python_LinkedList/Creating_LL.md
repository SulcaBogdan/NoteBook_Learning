# Crearea unui linked list

Primul pas este sa definim clasa pentru nod care va contine cele doua proprietati, respectiv data(informatia) si referinta catre urmatorul nod:

```python
class Node:
    def __init__(self, data):
        self.data = data
        self.next = None
```

Am definit clasa `Node` cu constructorul care primeste ca argument `data` si o proprietata initializate `next` cu `None` deoarece dacă avem un singur nod atunci nu există nimic în referința lui.

Dupa crearea clasei pentru noduri urmeaza sa definim clasa pentru LinkedList.

```python
class LinkedList:
    def __init__(self):
        self.head = None
```

Am definit clasa `LinkedList` pentru a initializa o lista goala. `self.head = None` indica faptul ca la inceput, lista nu contine nici un element. Acum ca avem clasa pentru nod si clasa pentru LinkedList trebuie doar sa adaugam metode pentru adaugare , stergere, inlocuire etc.

## Inserare intr-un linked list

Exemplu de metoda pentru inserarea unui nod la inceputul linked list:

```python
def insertAtBegin(self, data):
    new_node = Node(data)
    if self.head is None:
        self.head = new_node
        return
    else:
        new_node.next = self.head
        self.head = new_node
```

Aceasta metoda primeste ca argument `data` care reprezinta valoarea pe care vrem sa o adaugam in lista.

Initializam un obiect de `Node` cu denumirea `new_node` si ca paramentru introducem valoarea `data` din metoda.

Verificam daca `head` exista (daca este None), daca `head` este `None` atunci obiectul node (valoarea noastra) va devenii `head`, si oprim metoda, dar daca `head` exista deja (nu este `None`) atunci vom atribui urmatoarului nod din lista valoarea lui `head` si noul `head` va devenii `new_node` valoarea introdusa de noi.

Acesta a fost un exemplu de adaugare a unui `nod`(valoarea noastra) la inceputul listei.

### Putem insera un nod intr-o pozitie specifica intr-un linked list? Da!

## Inserarea intr-o pozitie specifica din linked list.

```python
def insertAtIndex(self, data, index):
    new_node = Node(data)
    current_node = self.head
    position = 0
    if position == index:
        self.insertAtBegin(data)
    else:
        while(current_node != None and position+1 != index):
            position = position+1
            current_node = current_node.next

        if current_node != None:

            new_node.next = current_node.next
            current_node.next = new_node
        else:
            print("Index not present")
```