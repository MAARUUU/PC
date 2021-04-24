# Потоки в С#
Поток — это по сути последовательность инструкций, которые выполняются параллельно с другими потоками. Каждая программа создает по меньшей мере один поток: *основной*, который запускает функцию main(). Программа, использующая только главный поток, является *однопоточной*; если добавить один или более потоков, она станет *многопоточной*.  
Потоки — это способ сделать несколько вещей одновременно. Это может быть полезно, например, для отображения анимации и обработки пользовательского ввода данных во время загрузки изображений или звуков. Потоки также широко используется в сетевом программировании, во время ожидания получения данные будет продолжаться обновление и рисование приложения.   
Используя класс **Thread**, мы можем выделить в приложении несколько потоков, которые будут выполняться одновременно.  
Во-первых, для запуска нового потока нам надо определить задачу в приложении, которую будет выполнять данный поток. Для этого мы можем добавить новый метод, производящий какие-либо действия.  
Для создания нового потока используется делегат **ThreadStart**, который получает в качестве параметра выполняемый метод. И чтобы запустить поток, вызывается метод **Start**.
```c#
       // создаем новый поток
        Thread myThread = new Thread(new ThreadStart(Count));
        myThread.Start(); // запускаем поток
 ...................

      public static void Count()
       {
          for (int i = 1; i < 9; i++)
         {
            Console.WriteLine("Второй поток:");
            Console.WriteLine(i * i);
            Thread.Sleep(400);
         }
       }
```  
Здесь новый поток будет производить действия, определенные в методе Count. В данном случае это возведение в квадрат числа и вывод его на экран. И после каждого умножения с помощью метода **Thread.Sleep** мы усыпляем поток на 400 миллисекунд.  
# Потоки с параметрами
# Как передать данные в функцию потока
Для этой цели используется делегат **ParameterizedThreadStart**.  

## Thread(ParameterizedThreadStart)   
Инициализирует новый экземпляр класса Thread, при этом указывается делегат, позволяющий объекту быть переданным в поток при запуске потока.
```csharp
public Thread (System.Threading.ParameterizedThreadStart start);
```
Параметры  
---
start(ParameterizedThreadStart) - Делегат, указывающий на методы, которые вызываются при запуске потока.
# Примеры 
В следующем примере показан синтаксис для создания и использования ParameterizedThreadStart делегата с статическим методом и методом экземпляра.
```csharp
using System;
using System.Threading;

public class Work
{
    public static void Main()
    {
        // Start a thread that calls a parameterized static method.
        Thread newThread = new Thread(Work.DoWork);
        newThread.Start(42);

        // Start a thread that calls a parameterized instance method.
        Work w = new Work();
        newThread = new Thread(w.DoMoreWork);
        newThread.Start("The answer.");
    }
 
    public static void DoWork(object data)
    {
        Console.WriteLine("Static thread procedure. Data='{0}'",
            data);
    }

    public void DoMoreWork(object data)
    {
        Console.WriteLine("Instance thread procedure. Data='{0}'",
            data);
    }
}
```  
Поток не начинает выполняться при его создании. Чтобы запланировать выполнение потока, вызовите Start метод. Чтобы передать объект данных в поток, используйте Start(Object) перегрузку метода.  
Его действие похоже на функциональность делегата ThreadStart.  
Рассмотрим на примере:  
```c#
        int number = 4;
        // создаем новый поток
        Thread myThread = new Thread(new ParameterizedThreadStart(Count));
        myThread.Start(number); 
```  
После создания потока мы передаем метод myThread.Start(number); переменную, значение которой хотим передать в поток.   
Также существует **классовый подход,** он нужен нам, если нам надо передать не один, а несколько параметров различного типа. Сначала определяем специальный класс Counter, объект которого будет передаваться во второй поток, а в методе Main передаем его во второй поток.  
```c#
   class Program
  {
    static void Main(string[] args)
    {
        Counter counter = new Counter();
        counter.x = 4;
        counter.y = 5;
            
        Thread myThread = new Thread(new ParameterizedThreadStart(Count));
        myThread.Start(counter); 
 
        //...................
    }
 
    public static void Count(object obj)
    {
        for (int i = 1; i < 9; i++)
        {
            Counter c = (Counter)obj;
 
            Console.WriteLine("Второй поток:");
            Console.WriteLine(i*c.x *c.y);
        }
    }
 }
 
    public class Counter
    {
        public int x;
        public int y;
    }
```
# Как получить данные из функции потока?  
Значение, возвращаемое в функции, связанной с потоком thread, игнорируется, т.е. при имеющейся сигнатуре вернуть его в main не получится.  
Нужно либо передать его как **ссылочный аргумент ref с модификацией сигнатуры и последующим ожиданием завершения потока через join**, либо использовать **async**.
```c#
static void Main(string[] args)
{
     Thread myThread = new Thread();
     myThread.Start(Count,ref(er)); 
}
```  
Пример async в С++ :  
```c
auto fut = async(tr,a,b);
...
int result = fut.get();
```  
### Извлечение данных из потоков с помощью методов обратного вызова 
---  
Приведенный ниже пример демонстрирует метод обратного вызова, который получает данные из потока. Конструктор класса, содержащего данные и метод потока, также принимает делегат, который представляет метод обратного вызова. Метод потока перед завершением своей работы вызывает этот делегат обратного вызова.  
```csharp
using System;
using System.Threading;

// The ThreadWithState класс содержит информацию, необходимую для
// задача, метод, выполняющий задачу, и делегат
// вызвать, когда задача будет выполнена.
//
public class ThreadWithState
{
    // Информация о состоянии, используемая в задаче.
    private string boilerplate;
    private int numberValue;

    // Делегат, используемый для выполнения метода обратного вызова, когда
    // задача выполнена.
    private ExampleCallback callback;

    // Конструктор получает информацию о состоянии и
     // делегат обратного вызова.
    public ThreadWithState(string text, int number,
        ExampleCallback callbackDelegate)
    {
        boilerplate = text;
        numberValue = number;
        callback = callbackDelegate;
    }

    // Процедура потока выполняет задачу, например
    // форматируем и печатаем документ, а затем вызываем
    // делегат обратного вызова с количеством напечатанных строк.
    public void ThreadProc()
    {
        Console.WriteLine(boilerplate, numberValue);
        if (callback != null)
            callback(1);
    }
}
// Делегат, определяющий подпись для метода обратного вызова.
//
public delegate void ExampleCallback(int lineCount);

// Точка входа для примера.
//
public class Example
{
    public static void Main()
    {
        // Предоставляем информацию о состоянии, необходимую для задачи.
        ThreadWithState tws = new ThreadWithState(
            "This report displays the number {0}.",
            42,
            new ExampleCallback(ResultCallback)
        );

        Thread t = new Thread(new ThreadStart(tws.ThreadProc));
        t.Start();
        Console.WriteLine("Main thread does some work, then waits.");
        t.Join();
        Console.WriteLine(
            "Independent task has completed; main thread ends.");
    }

   // Метод обратного вызова должен соответствовать подписи
   // делегат обратного вызова.
    //
    public static void ResultCallback(int lineCount)
    {
        Console.WriteLine(
            "Independent task printed {0} lines.", lineCount);
    }
}
```  
## **В C# нет класса, который используется для организации вычислений в потоке.** Но аналог всё-таки существует - ThreadStart Delegate.
## ThreadStart Delegate 
---
Представляет метод, который выполняется в отношении Thread.  
Вместо того, чтобы создавать подклассы класса Thread, мы просто создаем новый объект System.Threading.Thread и передаем ему делегат ThreadStart (это функция, в которой мы выполняем работу).  
```csharp
public delegate void ThreadStart();
```
# Пример  
В следующем примере кода показан синтаксис для создания и использования ThreadStart делегата с методом экземпляра и со статическим методом.
```c#
using System;
using System.Threading;

class Test
{
    static void Main() 
    {
        // Чтобы запустить поток с использованием процедуры статического потока, используйте
        // имя класса и имя метода при создании ThreadStart
        // делегат. Начиная с версии 2.0 .NET Framework,
        // явно создавать делегат не нужно.
        // Указываем имя метода в конструкторе Thread,
        // и компилятор выбирает правильный делегат. Например:
        // Thread newThread = new Thread(Work.DoWork);
        //
        ThreadStart threadDelegate = new ThreadStart(Work.DoWork);
        Thread newThread = new Thread(threadDelegate);
        newThread.Start();

        // Чтобы запустить поток, используя метод экземпляра для потока
        // процедура, используйте переменную экземпляра и имя метода, когда
        // вы создаете делегат ThreadStart. Начиная с версии
        // 2.0 .NET Framework явный делегат не
        // обязательный.
        //
        Work w = new Work();
        w.Data = 42;
        threadDelegate = new ThreadStart(w.DoMoreWork);
        newThread = new Thread(threadDelegate);
        newThread.Start();
    }
}

class Work 
{
    public static void DoWork() 
    {
        Console.WriteLine("Static thread procedure."); 
    }
    public int Data;
    public void DoMoreWork() 
    {
        Console.WriteLine("Instance thread procedure. Data={0}", Data); 
    }
}
``` 
При создании управляемого потока метод, выполняемый в потоке, представляется ThreadStart делегатом или ParameterizedThreadStart делегатом, который передается в Thread конструктор. Поток не начинает выполняться до Thread.Start вызова метода. Выполнение начинается с первой строки метода, представленного ThreadStart ParameterizedThreadStart делегатом.
