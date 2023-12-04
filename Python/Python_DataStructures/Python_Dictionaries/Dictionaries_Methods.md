# Metodele dictionarelor

| Metodă        | Descriere                                                                       | Exemplu                                                                                       |
|---------------|---------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------|
| clear()       | Elimină toate elementele din dicționar                                           | `dictionar = {'a': 1, 'b': 2}` <br> `dictionar.clear()` <br> `print(dictionar)` va afișa `{}` |
| copy()        | Returnează o copie a dicționarului                                              | `dictionar = {'a': 1, 'b': 2}` <br> `copie_dictionar = dictionar.copy()`                        |
| fromkeys()    | Returnează un dicționar cu cheile și valoarea specificate                        | `chei = ['a', 'b', 'c']` <br> `valoare = 0` <br> `dictionar = dict.fromkeys(chei, valoare)` |
| get()         | Returnează valoarea cheii specificate                                            | `dictionar = {'a': 1, 'b': 2}` <br> `valoare = dictionar.get('a')` <br> `print(valoare)` va afișa `1` |
| items()       | Returnează o listă conținând un tuplu pentru fiecare pereche cheie-valoare      | `dictionar = {'a': 1, 'b': 2}` <br> `elemente = dictionar.items()` <br> `print(elemente)` va afișa `[('a', 1), ('b', 2)]` |
| keys()        | Returnează o listă conținând cheile dicționarului                                | `dictionar = {'a': 1, 'b': 2}` <br> `chei = dictionar.keys()` <br> `print(chei)` va afișa `['a', 'b']` |
| pop()         | Elimină elementul cu cheia specificată                                           | `dictionar = {'a': 1, 'b': 2}` <br> `valoare = dictionar.pop('a')` <br> `print(valoare)` va afișa `1` |
| popitem()     | Elimină ultima pereche cheie-valoare inserată                                    | `dictionar = {'a': 1, 'b': 2}` <br> `pereche = dictionar.popitem()` <br> `print(pereche)` va afișa `('b', 2)` |
| setdefault()  | Returnează valoarea cheii specificate. Dacă cheia nu există, o inserează cu valoarea specificată | `dictionar = {'a': 1, 'b': 2}` <br> `valoare = dictionar.setdefault('c', 0)` <br> `print(dictionar)` va afișa `{'a': 1, 'b': 2, 'c': 0}` |
| update()      | Actualizează dicționarul cu perechile cheie-valoare specificate                 | `dictionar1 = {'a': 1, 'b': 2}` <br> `dictionar2 = {'b': 3, 'c': 4}` <br> `dictionar1.update(dictionar2)` <br> `print(dictionar1)` va afișa `{'a': 1, 'b': 3, 'c': 4}` |
| values()      | Returnează o listă a tuturor valorilor din dicționar                             | `dictionar = {'a': 1, 'b': 2}` <br> `valori = dictionar.values()` <br> `print(valori)` va afișa `[1, 2]` |
