# Métodos Útiles para Arrays en c#

### 1: Bucket Sort (Ordenación de cubo):

La ordenación de cubos es un algoritmo de ordenación por comparación que opera en elementos dividiéndolos en diferentes cubos y luego ordenando estos cubos individualmente. Cada depósito se ordena individualmente utilizando un algoritmo de ordenación independiente, como la ordenación por inserción, o aplicando el algoritmo de ordenación de cubos de forma recursiva.

La ordenación de cubos es principalmente útil cuando la entrada se distribuye uniformemente en un rango. Por ejemplo, imagina que tienes una gran variedad de enteros de punto flotante distribuidos uniformemente entre un límite superior e inferior.

Puedes usar otro algoritmo de ordenación, como la ordenación por combinación, la ordenación por montones o la ordenación rápida. Sin embargo, esos algoritmos garantizan una complejidad de tiempo en el mejor de los casos de `O(nlogn)`.

Usando la ordenación de cubos, la ordenación del mismo arreglo se puede completar a `O(n)`tiempo.

*Ejemplo:*

```csharp
using System;
using System.Collections.Generic;

class Program
{
    static void Main()
    {
        double[] numeros = { 0.42, 0.32, 0.23, 0.52, 0.25, 0.47, 0.51 };

        double[] resultado = BucketSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", resultado));
    }

    static double[] BucketSort(double[] array)
    {
        int n = array.Length;
        List<double>[] buckets = new List<double>[n];

        for (int i = 0; i < n; i++)
        {
            buckets[i] = new List<double>();
        }

        foreach (double num in array)
        {
            int index = (int)(n * num);
            buckets[index].Add(num);
        }

        List<double> resultado = new List<double>();
        foreach (var bucket in buckets)
        {
            bucket.Sort();
            resultado.AddRange(bucket);
        }

        return resultado.ToArray();
    }
}

// resultado: Array ordenado: 0,23, 0,25, 0,32, 0,42, 0,47, 0,51, 0,52

```

### 2: Counting Sort (Ordenación de conteo):

El algoritmo de ordenación por conteo funciona creando primero una lista de los conteos u ocurrencias de cada valor único en la lista. Luego crea una lista ordenada final basada en la lista de conteos.

Una cosa importante que debes recordar es que la ordenación por conteo solo se puede usar cuando conoces de antemano el rango de valores posibles en la entrada.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 4, 2, 2, 8, 3, 3, 1 };

        CountingSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void CountingSort(int[] array)
    {
        int max = array[0];
        foreach (int num in array)
        {
            if (num > max) max = num;
        }

        int[] conteo = new int[max + 1];

        foreach (int num in array)
        {
            conteo[num]++;
        }

        int index = 0;
        for (int i = 0; i < conteo.Length; i++)
        {
            while (conteo[i] > 0)
            {
                array[index++] = i;
                conteo[i]--;
            }
        }
    }
}
// Array ordenado: 1, 2, 2, 3, 3, 4, 8
```

### 3: Insertion Sort (Ordenación de inserción):

La ordenación por inserción es un algoritmo de ordenación simple para una pequeña cantidad de elementos.

En la ordenación por inserción, compara el elemento con los elementos anteriores. Si los elementos anteriores son mayores que el elemento seleccionado, mueve el elemento anterior a la siguiente posición.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 5, 3, 4, 1, 2 };

        InsertionSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void InsertionSort(int[] array)
    {
        for (int i = 1; i < array.Length; i++)
        {
            int actual = array[i];
            int j = i - 1;

            while (j >= 0 && array[j] > actual)
            {
                array[j + 1] = array[j];
                j--;
            }

            array[j + 1] = actual;
        }
    }
}
// Array ordenado: 1, 2, 3, 4, 5
```

### 3: Heap Sort (Ordenación por montones):

Heapsort es un algoritmo de ordenación eficiente basado en el uso de montones máximos/mínimos. Un montón es una estructura de datos basada en un árbol que satisface la propiedad del montón, es decir, para un montón máximo, la clave de cualquier nodo es menor o igual que la clave de su padre (si tiene un padre).

Esta propiedad se puede aprovechar para acceder al elemento máximo en el montón en tiempo O (logn) usando el método maxHeapify. Realizamos esta operación n veces, cada vez que movemos el elemento máximo en el montón a la parte superior del montón y lo extraemos del montón y lo colocamos en un arreglo ordenado. Por lo tanto, después de n iteraciones, tendremos una versión ordenada del arreglo de entrada.

El algoritmo no es un algoritmo en el lugar y requeriría que se construyera primero una estructura de datos de montón. El algoritmo también es inestable, lo que significa que al comparar objetos con la misma clave, no se conservará el orden original.

Este algoritmo se ejecuta en tiempo O(nlogn) y espacio adicional O(1) [O(n) incluido el espacio requerido para almacenar los datos de entrada] ya que todas las operaciones se realizan completamente en el lugar.

La complejidad de tiempo del caso mejor, peor y promedio de Heapsort es O (nlogn). Aunque heapsort tiene una mejor complejidad en el peor de los casos que quicksort, una ordenación rápida bien implementada se ejecuta más rápido en la práctica. Este es un algoritmo basado en la comparación, por lo que se puede usar para conjuntos de datos no numéricos en la medida en que se pueda definir alguna relación (propiedad del montón) sobre los elementos.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 4, 10, 3, 5, 1 };

        HeapSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void HeapSort(int[] array)
    {
        int n = array.Length;

        for (int i = n / 2 - 1; i >= 0; i--)
        {
            Heapify(array, n, i);
        }

        for (int i = n - 1; i >= 0; i--)
        {

            int temp = array[0];
            array[0] = array[i];
            array[i] = temp;

            // Reajustar heap reducido
            Heapify(array, i, 0);
        }
    }

    static void Heapify(int[] array, int n, int i)
    {
        int mayor = i;         
        int izq = 2 * i + 1;   
        int der = 2 * i + 2;   

        if (izq < n && array[izq] > array[mayor])
        {
            mayor = izq;
        }

        if (der < n && array[der] > array[mayor])
        {
            mayor = der;
        }

        if (mayor != i)
        {
            int temp = array[i];
            array[i] = array[mayor];
            array[mayor] = temp;

            Heapify(array, n, mayor);
        }
    }
}
// Array ordenado:1, 3, 4, 5, 10
```

### 4: Ordenación Radix:

**Requisito previo: Ordenar por conteo*

QuickSort, MergeSort y HeapSort son algoritmos de ordenación basados ​​en comparaciones. CountSort no lo es. Tiene la complejidad de O(n+k), donde k es el elemento máximo del arreglo de entrada. Entonces, si k es O(n), CountSort se convierte en una ordenación lineal, que es mejor que los algoritmos de ordenación basados ​​en comparación que tienen una complejidad de tiempo O(nlogn).

La idea es extender el algoritmo CountSort para obtener una mejor complejidad de tiempo cuando k pasa a O(n2). Aquí viene la idea de Radix Sort.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 170, 45, 75, 90, 802, 24, 2, 66 };

        RadixSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void RadixSort(int[] array)
    {

        int max = array[0];
        foreach (int num in array)
        {
            if (num > max) max = num;
        }

        for (int exp = 1; max / exp > 0; exp *= 10)
        {
            CountingSortPorDigito(array, exp);
        }
    }

    static void CountingSortPorDigito(int[] array, int exp)
    {
        int n = array.Length;
        int[] output = new int[n];    
        int[] count = new int[10];    

        for (int i = 0; i < n; i++)
        {
            int digito = (array[i] / exp) % 10;
            count[digito]++;
        }

        for (int i = 1; i < 10; i++)
        {
            count[i] += count[i - 1];
        }

        for (int i = n - 1; i >= 0; i--)
        {
            int digito = (array[i] / exp) % 10;
            output[count[digito] - 1] = array[i];
            count[digito]--;
        }

        for (int i = 0; i < n; i++)
        {
            array[i] = output[i];
        }
    }
}
// Array ordenado: 2, 24, 45, 66, 75, 90, 170, 802
```

### 5: Selection Sort (Ordenaión por selección):

Selection Sort es uno de los algoritmos de ordenación más simples. Este algoritmo recibe su nombre de la forma en que itera a través del arreglo: Selecciona el elemento más pequeño actual y lo cambia de lugar.

Así es como funciona:

1. Encuentra el elemento más pequeño en el arreglo y lo intercambia con el primer elemento.
2. Encuentra el segundo elemento más pequeño y lo intercambia con el segundo elemento del arreglo.
3. Encuentra el tercer elemento más pequeño y lo intercambia con el tercer elemento del arreglo.
4. Repite el proceso de encontrar el siguiente elemento más pequeño y cambiarlo a la posición correcta hasta que se ordene todo el arreglo.

Pero, ¿cómo escribirías el código para encontrar el índice del segundo valor más pequeño en un arreglo?

Una manera fácil es notar que el valor más pequeño ya se ha cambiado al índice 0, por lo que el problema se reduce a encontrar el elemento más pequeño en el arreglo que comienza en el índice 1.

La ordenación por selección siempre toma el mismo número de comparaciones clave — N(N − 1)/2.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 29, 10, 14, 37, 13 };

        SelectionSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void SelectionSort(int[] array)
    {
        int n = array.Length;

        for (int i = 0; i < n - 1; i++)
        {
            int minIndex = i;

            for (int j = i + 1; j < n; j++)
            {
                if (array[j] < array[minIndex])
                {
                    minIndex = j;
                }
            }

            if (minIndex != i)
            {
                int temp = array[i];
                array[i] = array[minIndex];
                array[minIndex] = temp;
            }
        }
    }
}
// Array ordenado: 10, 13, 14, 29, 37
```

### 6: Bubble Sort (Ordenaión de burbuja):

Al igual que las burbujas se elevan desde el fondo de un vaso, ****la** ordenación **de burbujas**** es un algoritmo simple que ordena una lista, lo que permite que los valores más bajos o más altos aparezcan en la parte superior. El algoritmo atraviesa una lista y compara valores adyacentes, intercambiandolos si no están en el orden correcto.

Con una complejidad en el peor de los casos de O(n^2), la ordenación de burbujas es muy lenta en comparación con otros algoritmos de ordenación como la ordenación rápida. La ventaja es que es uno de los algoritmos de ordenación más fáciles de entender y codificar desde cero.

Desde una perspectiva técnica, la ordenación por burbuja es razonable para ordenar arreglos de tamaño pequeño o especialmente cuando se ejecutan algoritmos de ordenación en ordenadores con recursos de memoria notablemente limitados.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 5, 3, 8, 4, 2 };

        BubbleSort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void BubbleSort(int[] array)
    {
        int n = array.Length;
        bool huboCambios;

        do
        {
            huboCambios = false;

            for (int i = 0; i < n - 1; i++)
            {
                if (array[i] > array[i + 1])
                {
                    int temp = array[i];
                    array[i] = array[i + 1];
                    array[i + 1] = temp;

                    huboCambios = true;
                }
            }

            n--;

        } while (huboCambios);
    }
}
// Array ordenado: 2, 3, 4, 5, 8
```

### 7: Ordenación rápida:

Al igual que las burbujas se elevan desde el fondo de un vaso, ****la** ordenación **de burbujas**** es un algoritmo simple que ordena una lista, lo que permite que los valores más bajos o más altos aparezcan en la parte superior. El algoritmo atraviesa una lista y compara valores adyacentes, intercambiandolos si no están en el orden correcto.

Con una complejidad en el peor de los casos de O(n^2), la ordenación de burbujas es muy lenta en comparación con otros algoritmos de ordenación como la ordenación rápida. La ventaja es que es uno de los algoritmos de ordenación más fáciles de entender y codificar desde cero.

Desde una perspectiva técnica, la ordenación por burbuja es razonable para ordenar arreglos de tamaño pequeño o especialmente cuando se ejecutan algoritmos de ordenación en ordenadores con recursos de memoria notablemente limitados.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 10, 7, 8, 9, 1, 5 };

        QuickSort(numeros, 0, numeros.Length - 1);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void QuickSort(int[] array, int inicio, int fin)
    {
        if (inicio < fin)
        {
            int indicePivote = Particionar(array, inicio, fin);

            QuickSort(array, inicio, indicePivote - 1);
            QuickSort(array, indicePivote + 1, fin); 
        }
    }

    static int Particionar(int[] array, int inicio, int fin)
    {
        int pivote = array[fin]; 
        int i = inicio - 1; 

        for (int j = inicio; j < fin; j++)
        {
            if (array[j] <= pivote)
            {
                i++;
  
                int temp = array[i];
                array[i] = array[j];
                array[j] = temp;
            }
        }

        int temp2 = array[i + 1];
        array[i + 1] = array[fin];
        array[fin] = temp2;

        return i + 1;
    }
}
// Array ordenado: 1, 5, 7, 8, 9, 10
```

### 8: Timsort:

Al igual que las burbujas se elevan desde el fondo de un vaso, ****la** ordenación **de burbujas**** es un algoritmo simple que ordena una lista, lo que permite que los valores más bajos o más altos aparezcan en la parte superior. El algoritmo atraviesa una lista y compara valores adyacentes, intercambiandolos si no están en el orden correcto.

Con una complejidad en el peor de los casos de O(n^2), la ordenación de burbujas es muy lenta en comparación con otros algoritmos de ordenación como la ordenación rápida. La ventaja es que es uno de los algoritmos de ordenación más fáciles de entender y codificar desde cero.

Desde una perspectiva técnica, la ordenación por burbuja es razonable para ordenar arreglos de tamaño pequeño o especialmente cuando se ejecutan algoritmos de ordenación en ordenadores con recursos de memoria notablemente limitados.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 5, 2, 9, 1, 5, 6 };

        Array.Sort(numeros);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }
}
// Array ordenado: 1, 2, 5, 5, 6, 9
```

### 9: Mergesort (Ordenación por fusión):

Merge Sort es un algoritmo Divide y vencerás. Divide el arreglo de entrada en dos mitades, se llama a sí mismo para las dos mitades y luego fusiona las dos mitades ordenadas. La mayor parte del algoritmo tiene dos matrices ordenadas, y tenemos que fusionarlas en un único arreglo ordenado. Todo el proceso de ordenar un arreglo de N enteros se puede resumir en tres pasos:

* Divide el arreglo en dos mitades.
* Ordena la mitad izquierda y la mitad derecha usando el mismo algoritmo recurrente.
* Combina las mitades ordenadas.

Hay algo conocido como el algoritmo de dos dedos que nos ayuda a fusionar dos arreglos ordenados. El uso de esta subrutina y la llamada a la función de ordenación por fusión en las mitades del arreglo de forma recursiva nos dará el arreglo ordenado final que estamos buscando.

Dado que este es un algoritmo basado en la recursión, tenemos una relación de recurrencia para él. Una relación de recurrencia es simplemente una forma de representar un problema en términos de sus subproblemas.

*`T(n) = 2 * T(n / 2) + O(n)`*

Poniéndolo en lenguaje sencillo, dividimos el subproblema en dos partes en cada paso y tenemos una cantidad lineal de trabajo que tenemos que hacer para unir las dos mitades ordenadas en cada paso.

*Ejemplo:*

```csharp
using System;

class Program
{
    static void Main()
    {
        int[] numeros = { 38, 27, 43, 3, 9, 82, 10 };

        MergeSort(numeros, 0, numeros.Length - 1);

        Console.WriteLine("Array ordenado:");
        Console.WriteLine(string.Join(", ", numeros));
    }

    static void MergeSort(int[] array, int izquierda, int derecha)
    {
        if (izquierda < derecha)
        {
            int medio = (izquierda + derecha) / 2;

            MergeSort(array, izquierda, medio);
            MergeSort(array, medio + 1, derecha);

            Fusionar(array, izquierda, medio, derecha);
        }
    }

    static void Fusionar(int[] array, int izquierda, int medio, int derecha)
    {
        int n1 = medio - izquierda + 1;
        int n2 = derecha - medio;

        int[] L = new int[n1];
        int[] R = new int[n2];

        for (int i = 0; i < n1; i++)
            L[i] = array[izquierda + i];
        for (int j = 0; j < n2; j++)
            R[j] = array[medio + 1 + j];

        int a = 0, b = 0;
        int k = izquierda;

        while (a < n1 && b < n2)
        {
            if (L[a] <= R[b])
            {
                array[k] = L[a];
                a++;
            }
            else
            {
                array[k] = R[b];
                b++;
            }
            k++;
        }

        while (a < n1)
        {
            array[k] = L[a];
            a++;
            k++;
        }

        while (b < n2)
        {
            array[k] = R[b];
            b++;
            k++;
        }
    }
}
// Array ordenado: 3, 9, 10, 27, 38, 43, 82
```


