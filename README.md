# Гайд по Antrl

## Введение 

Данный гайд посвящен практике по Antlr. Вначале мы установим необходимые инструменты и разберемся, как написать свой первый компилятор. 

## Инструменты 

### Java
Так как Antrl написан на Java, для его работы потребуется сначала установить Java. 
Заходим на этот [сайт](https://java.com/en/download/) и устанавливаем.

### IntelliJ IDEA 
Нам понадобится данный инструмент для написания грамматики и построения дерева по этой грамматике.
Для его установки потребуется создать аккаунт на сайте JetBrains [JetBrains Products for Learning](https://www.jetbrains.com/shop/eform/students) и скачать [IntelliJ IDEA](https://www.jetbrains.com/idea/).

### Плагин Antlr v4 для IDEA
Этот плагин поможет  нам написать грамматику в IDEA и сгенерировать код для C#.
1. Необходимо сначала скачать этот плагин с этого сайта [ANTLR v4 grammar plugin :: JetBrains Plugin Repository](https://plugins.jetbrains.com/plugin/7358-antlr-v4-grammar-plugin).
2. Запускаем IDEA и открываем настройки  `⌘,`.
3. Выбираем вкладку *Plugins*.
4. Нажимаем на *Install plugin from disk..* и указываем путь к скаченному архиву. 
5. Кликаем на *OK* в настройках и перезагружаем IntelliJ IDEA.
6. Создаем новый  проект, добавляем в папку `scr` файл в формате `*.g4`  и пишем грамматику.
---
## Генерация кода C# :yellow_heart: :yellow_heart: :yellow_heart:
Следующем шагом после написании грамматики является генерация кода для C#. Для этого необходимо
1. Необходимо загрузить [Antlr-4.5.jar](https://github.com/vietngn7/Antlr/raw/master/antlr-4.5.3-complete.jar).
2. Переместить его в папку с грамматикой (файл `.g4`).
3. Сгенерировать файлы для C#
	1. *Windows*
		1. Создать в папке с грамматикой текстовой файл `gen.bat` .
		2. Вставить туда `java -jar antlr-4.5.3-complete.jar -Dlanguage=CSharp -o src <filename>.g4`, где filename - название вашей грамматики.`
		3. Запустить `gen.bat`.
	2. *macOS*
		1. Запустить Терминал (Terminal)
```
	cd <path> # где path - путь к папке с грамматикой
	java -jar antlr-4.5.3-complete.jar -Dlanguage=CSharp -o src <filename>.g4 # где filename - название вашей грамматики.
```
4. Создать новый C# проект и добавить сгенерированные файлы из папки `scr` к проекту.
5. Загрузить [Antlr4.Runtime.dll](https://github.com/vietngn7/Antlr/raw/master/Antlr4.Runtime.dll) и подключить к его проекту.
6. Реализовать интерфейс  `<grammar>BaseListener.cs`.

Класс Listener нам понадобится для трансляции кода с `<SomeLanguage>` на C#.
>Q11: Цепочка трансляции.
>
>A11:
>Например, для транслятора для входного языка Basic (.bas):
>
>BasTranslator.g4[Grammar] => (ANTLR) => BasTranslator*.java => (javac) => BasTranslator.jar
>
>test1.bas=>(BasTranslator.jar[Translator])=>test1.cs=>(csc.exe)=>test1.exe
>
>test2.bas=>(BasTranslator.jar[Translator])=>test2.cs=>(csc.exe)=>test2.exe

Пример реализация Listener [Яндекс.Диск](https://yadi.sk/d/8KJSyWHN3Khhd2)


## Полезные материалы 
1. [The ANTLR mega tutorial - Federico Tomassetti - Software Architect](https://tomassetti.me/antlr-mega-tutorial/#creating-a-grammar) очень хороший туториал по Antlr с кодом для C#.
2. [antlr4/grammars.md at 4.6 · antlr/antlr4 · GitHub](https://github.com/antlr/antlr4/blob/4.6/doc/grammars.md) как писать грамматику
3. Материалы Дворяна
