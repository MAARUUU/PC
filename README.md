# Конспект
## **Инспекция кода**

**Code Review** ( Инспекция кода ) — это неотъемлемая часть процесса разработки, придуманная для снижения технических недоработок и обеспечения постоянства кодовой базы.  
*Цель проверки* – обнаружение и исправление ошибок, которые были пропущены, остались незамечены при разработке.  
*Результат инспекции* как правило – улучшение качество ПО и навыки разработчика.  
### Инспекция кода  состоит из нескольких этапов.
- Сначала разработчик добавляет новую функциональность в код и извещает остальных участников о том, что нужно проверить эти обновления.  
- На втором этапе члены команды отсматривают код и оставляют свои комментарии.   
- Дальше следует работа с замечаниями. Если автор не согласен с  какой-то претензией, он может её отклонить, но для этого предстоит привести убедительные аргументы в защиту своей позиции. Если аргументов нет, он делает нужные исправления.  
- Дальше всё повторяется сначала и происходит систематически — каждый раз, когда в код вносится новая порция изменений.   
   
## **Плюсы Code Review:**
- Code Review помогает на ранних стадиях находить некоторые ошибки и избавляться от запутанных решений. В работе над кодом участвует не один человек, а целая команда, поэтому часто может появиться свежий взгляд со стороны.
- Программист, который заранее знает, что коллеги проверят его работу, стремится писать более аккуратно и организованно. На выходе получается код, который понимают несколько человек, а значит, он намного ближе к качественному.
- Когда группа из нескольких специалистов знакома с кодом на высоком уровне, его становится легко передавать между участниками процесса.
## **Минусы Code Review:**
- Главный и единственный минус — его длительность. Всем участникам Code Review приходится тратить время на то, чтобы посмотреть и при необходимости прокомментировать код, а разработчику — на исправление ошибок.
## **Когда использовать Code Review?**
- Code Review **не нужен** в работе над простыми приложениями, которые делаются раз и навсегда.
- Если у вас есть планы по развитию приложения, добавлению новых функций и расширению аудитории, процесс Code Review поможет делать это быстрее, дешевле и эффективнее.
- Кроме того, Code Review **будет очень полезен**, если проект большой, и вы планируете подключать к нему новых разработчиков или передавать другой команде.  
---
### Источники:
- https://medium.com/nuances-of-programming/%D1%81%D0%BE%D0%B7%D0%B4%D0%B0%D0%BD%D0%B8%D0%B5-%D0%BF%D1%80%D0%B0%D0%B2%D0%B8%D0%BB%D1%8C%D0%BD%D0%BE%D0%B3%D0%BE-%D1%87%D0%B5%D0%BA-%D0%BB%D0%B8%D1%81%D1%82%D0%B0-%D0%B4%D0%BB%D1%8F-%D0%B8%D0%BD%D1%81%D0%BF%D0%B5%D0%BA%D1%86%D0%B8%D0%B8-%D0%BA%D0%BE%D0%B4%D0%B0-8e054c869ea8
- https://multiurok.ru/files/riev-iuirovaniie-proghrammnogho-koda.html
- https://itnan.ru/post.php?c=1&p=467293
- https://livetyping.com/ru/blog/chto-takoe-kachestvenny-kod-i-code-review         
---
# Отчёт
Инструменты статического анализа предназначены для выявления дефектов в исходном коде программ. Само название говорит, что принцип их работы основан на статическом анализе кода.  
Существует огромное количество инструментов статического анализа, созданных для различных языков программирования. 
## **C#**
- ReSharper. Плагин для Visual Studio, проводит статический анализ кода на языке C# и не только. Имеет 30-дневный триал.
- FxCop. Бесплатный инструмент для статического анализа кода от компании Microsoft. Производит анализ байт-кода (CIL) на соответствие рекомендациям Microsoft по проектированию приложений. На данный момент проект мертв.
- Roslyn Analyzers. Набор статических анализаторов кода для языков C# и Visual Basic на основе .Net Compiler Platform ("Roslyn"). Производит анализ исходного кода, в отличие от FxCop. В составе этого проекта также был произведен порт наиболее важных правил FxCop. 
- Security Code Scan. Статический анализатор кода на основе .Net Compiler Platform ("Roslyn") для языков C# и Visual Basic для поиска паттернов ошибок, связанных с безопасностью приложений: SQL Injection, Cross-Site Scripting (XSS), Cross-Site Request Forgery (CSRF), XML eXternal Entity Injection (XXE) и др. Производит анализ исходного кода.
- Roslynator. Набор статических анализаторов кода для языка C# на основе .Net Compiler Platform ("Roslyn"). Производит анализ исходного кода. 
- CodeRush. Плагин для Visual Studio. Продукт коммерческий, но имеется пробная версия.
- Parasoft dotTEST. Набор инструментов для тестирования приложений .NET, включающий в себя статический анализатор кода. Работает как плагин для Visual Studio. Как и в предыдущем случае, продукт коммерческий, имеется пробная версия.
---
## **ReSharper** 
---
ReSharper - дополнение (плагин), разработанное компанией JetBrains для повышения продуктивности работы в Microsoft Visual Studio.  
Проводит статический анализ кода (поиск ошибок в коде до компиляции) в масштабе всего решения, предусматривает дополнительные средства автозаполнения, навигации, поиска, подсветки синтаксиса, форматирования, оптимизации и генерации кода, предоставляет 40 автоматизированных рефакторингов, упрощает юнит-тестирование и др. Поддерживает языки программирования C# и VB.NET, а также предоставляет средства для работы с ASP.NET, ASP.NET MVC, XML, XAML, сценариями сборки NAnt и MSBuild.  

---
Cкачать - https://www.jetbrains.com/resharper/  

---
ReSharper помогает использовать структуру данных до того, как они формально определены.   
Например, создадим класс Person и дадим человеку имя и возраст.  
![title](/Image/pc1.PNG?raw=true "Optional Title") 
Наведя курсор мыши на класс Person и нажав Alt+Enter, ReSharper помогает создать класс без особых усилий.     
![title](/Image/pc2.PNG?raw=true "Optional Title") 
Также мы поступаем и со свойствами.        
![title](/Image/pc3.PNG?raw=true "Optional Title") 
ReSharper помогает обнаруживать ошибки еще до запуска кода. Одним из примеров является анализатор проверки орфографии. Скажем, вы создаете статический метод и случайно написали слово static как statc. Вы сможете увидеть эту орфографическую ошибку еще до запуска своего кода, потому что ReSharper выдаст предупреждение в вашем коде при вводе текста еще до завершения набора строки. Другими словами, вам не нужно производить сборку кода, чтобы узнать, что вы допустили ошибку.               
![title](/Image/pc6.PNG?raw=true "Optional Title") 
Либо вы написали метод, который начинается на строчную букву, то ReSharper подскажет вам, что его нужно исправить и предложит свои решения.  
![title](/Image/pc4.PNG?raw=true "Optional Title")   ![title](/Image/pc5.PNG?raw=true "Optional Title") 
 
