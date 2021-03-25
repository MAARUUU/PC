# Задание. Сеть Петри
Задана сеть Пери N = <P, T, I, O>.
Для своего варианта:    
1. Построить входную и выходную расширенные функции.
2. Построить граф.
3. Построить матрицу инцидентности  
```
Вариант 21
P={P1, P2, P3, P4, P5}
T={t1, t2, t3}
I(t1)={P1, P5}                     O(t1)={P2, P3 }
I(t2)={P1, P4, P4}                 O(t2)={P2}
I(t3)={P2, P3}                     O(t3)={P4, P5} 
```
```
 1. Входные и выходные расширенные функции: 
   I(P1)={ }                       O(P1)={t1, t2}
   I(P2)={t1, t2}                  O(P2)={t3}
   I(P3)={t1}                      O(P3)={t3}
   I(P4)={t3}                      O(P4)={t2, t2}
   I(P5)={t3}                      O(P5)={t1}        
```  
2.     
  ![title](/Image/petri.PNG?raw=true "Optional Title")
3. 
 Матрица входных и выходных инциденций:  
![title](/Image/mat1.PNG?raw=true "Optional Title")  ![title](/Image/mat2.PNG?raw=true "Optional Title")  
 Матрица инцидентности:  
 ![title](/Image/mat3.PNG?raw=true "Optional Title")    
