# Algoritmos de Ordenación en C#

Este repositorio presenta la implementación de los principales **algoritmos de ordenación** en el lenguaje **C#**, con ejemplos prácticos, explicaciones detalladas y observaciones sobre su rendimiento.
Autor: **Andrés Suárez**  

---

## 📚 Índice de Algoritmos

 1. Bubble Sort (Ordenación de burbuja)
 2. Selection Sort (Ordenación por selección)
 3. Insertion Sort (Ordenación por inserción)
 4. Merge Sort (Ordenación por fusión)
 5. Quick Sort (Ordenación rápida)
 6. Heap Sort (Ordenación por montones)
 7. Counting Sort (Ordenación por conteo)
 8. Radix Sort (Ordenación radix)
 9. Bucket Sort (Ordenación por cubos)
10. Timsort (Ordenación híbrida usada por defecto)

---

### 1. Bubble Sort
Algoritmo simple que compara elementos adyacentes e intercambia si están desordenados. Repite el proceso hasta que el array esté ordenado.

Complejidad:
🟢 Mejor caso: O(n)
🔴 Peor caso: O(n²)
✔️ Estable

### 2. Selection Sort
Busca el elemento más pequeño y lo coloca en la primera posición, repitiendo con el resto del array.

Complejidad:
🔴 O(n²) en todos los casos
❌ No estable

### 3. Insertion Sort
Toma cada elemento y lo "inserta" en la posición correcta respecto a los anteriores.

Complejidad:
🟢 O(n) mejor caso (ya ordenado)
🔴 O(n²) peor caso
✔️ Estable

### 4. Merge Sort
Divide el array en mitades recursivamente y luego fusiona de forma ordenada.

Complejidad:
🟢 O(n log n) en todos los casos
✔️ Estable
⚠️ Usa memoria adicional

### 5. Quick Sort
Selecciona un pivote y divide el array en menores y mayores al pivote, recursivamente.

Complejidad:
🟢 O(n log n) promedio
🔴 O(n²) peor caso (pivote malo)
❌ No estable
✅ Muy rápido en la práctica

### 6. Heap Sort
Convierte el array en un heap (montículo) y extrae el máximo sucesivamente.

Complejidad:
🟢 O(n log n)
❌ No estable
✅ No usa espacio adicional

### 7. Counting Sort
Ideal para enteros pequeños. Cuenta cuántas veces aparece cada número.

Complejidad:
🟢 O(n + k)
✔️ Estable
⚠️ No sirve con números negativos ni grandes rangos

### 8. Radix Sort
Ordena por cada dígito (unidad, decena, centena...) usando Counting Sort como base.

Complejidad:
🟢 O(nk) (n = elementos, k = dígitos)
✔️ Estable

### 9. Bucket Sort
Divide los elementos en "cubos", los ordena individualmente y los une.

Complejidad:
🟢 O(n + k) en promedio
✔️ Estable (depende de orden interno)
✅ Ideal para números decimales uniformes

### 10. Timsort
Usado internamente por Array.Sort() y List<T>.Sort() en C#. Mezcla Merge Sort + Insertion Sort optimizado.

Complejidad:
🟢 O(n log n)
🟢 O(n) mejor caso (parcialmente ordenado)
✔️ Estable
✅ Muy eficiente en la práctica
