---
title: "Como extrair o dia da semana de uma data específica"
description: "Como extrair o dia da semana de uma data específica"
keywords: .NET, .NET Core
author: stevehoag
ms.author: shoag
ms.date: 07/26/2016
ms.topic: article
ms.prod: .net
ms.technology: dotnet-standard
ms.devlang: dotnet
ms.assetid: 88a8f8b9-f5c9-4503-b968-84468b52bb8e
translationtype: Human Translation
ms.sourcegitcommit: 90fe68f7f3c4b46502b5d3770b1a2d57c6af748a
ms.openlocfilehash: 1b9d1d497524e62e5758c9be7be7b586a421a258
ms.lasthandoff: 03/03/2017

---

# <a name="how-to-extract-the-day-of-the-week-from-a-specific-date"></a>Como extrair o dia da semana de uma data específica

O .NET facilita a verificação da posição numérica do dia da semana em uma determinada data e a exibição do nome do dia localizado em uma determinada data. O valor enumerado que indica o dia da semana correspondente a uma determinada data está disponível na propriedade [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) ou [DateTimeOffset.DayOfWeek](xref:System.DateTimeOffset.DayOfWeek). Em contrapartida, para recuperar o nome do dia da semana é necessário realizar uma operação de formatação que pode ser executada com a chamada de um método de formatação, como o método `ToString` ou [String.Format](xref:System.String.Format(System.IFormatProvider,System.String,System.Object)) de valor de data e hora. Este tópico mostra como executar essas operações de formatação.

## <a name="to-extract-a-number-indicating-the-day-of-the-week-from-a-specific-date"></a>Para extrair um número que indique o dia da semana em uma determinada data

1. Se você estiver trabalhando com a representação de cadeia de caracteres de uma data, converta-a para um valor [DateTime](xref:System.DateTime) ou [DateTimeOffset](xref:System.DateTimeOffset) usando o método estático [DateTime.Parse](xref:System.DateTime.Parse(System.String)) ou [DateTimeOffset.Parse](xref:System.DateTimeOffset.Parse(System.String)).

2. Use a propriedade [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) ou [DateTimeOffset.DayOfWeek](xref:System.DateTimeOffset.DayOfWeek) para recuperar um valor [DayOfWeek](xref:System.DayOfWeek) que indica o dia da semana.

3. Se necessário, converta o valor [DayOfWeek](xref:System.DayOfWeek) para um número inteiro. 

O exemplo a seguir mostra um inteiro que representa o dia da semana de uma determinada data. 

```csharp
using System;

public class Example
{
   public static void Main()
   {
      DateTime dateValue = new DateTime(2008, 6, 11);
      Console.WriteLine((int) dateValue.DayOfWeek);      
   }
}
// The example displays the following output:
//       3
```

```vb
Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#
      Console.WriteLine(dateValue.DayOfWeek)           
   End Sub
End Module
' The example displays the following output:
'    3
```

## <a name="to-extract-the-abbreviated-weekday-name-from-a-specific-date"></a>Para extrair o nome do dia da semana abreviado de uma determinada data

1. Se você estiver trabalhando com a representação de cadeia de caracteres de uma data, converta-a para um valor [DateTime](xref:System.DateTime) ou [DateTimeOffset](xref:System.DateTimeOffset) usando o método estático [DateTime.Parse](xref:System.DateTime.Parse(System.String)) ou [DateTimeOffset.Parse](xref:System.DateTimeOffset.Parse(System.String)).

2. Você pode extrair o nome de dia da semana abreviado da cultura atual ou de uma cultura específica:

    a. Para extrair o nome de dia da semana abreviado da cultura atual, chame o método de instância [DateTime.ToString(String)](xref:System.DateTimeSystem.DateTime.ToString(System.String) ou [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) dos valores de data e hora e apresente a cadeia de caracteres "ddd" como o parâmetro *format*. O exemplo a seguir ilustra a chamada para o método `ToString(String)`.
    
```csharp
using System;

public class Example
{
   public static void Main()
   {
  DateTime dateValue = new DateTime(2008, 6, 11);
  Console.WriteLine(dateValue.ToString("ddd"));   
   }
}
// The example displays the following output:
//       Wed
```

```vb
Module Example
   Public Sub Main()
  Dim dateValue As Date = #6/11/2008#
      Console.WriteLine(dateValue.ToString("ddd"))    
   End Sub
End Module
' The example displays the following output:
'       Wed
```

    b. To extract the abbreviated weekday name for a specific culture, call the date and time value’s [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) or [DateTimeOffset.ToString(String, IFormatProvider)](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) instance method. Pass the string "ddd" as the *format* parameter. Pass either a [CultureInfo](xref:System.Globalization.CultureInfo) or a [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) object that represents the culture whose weekday name you want to retrieve as the *provider* parameter. The following code illustrates a call to the [ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) method using a [CultureInfo](xref:System.Globalization.CultureInfo) object that represents the fr-FR culture.
    
```csharp
using System;
using System.Globalization;

public class Example
{
    public static void Main()
    {
        DateTime dateValue = new DateTime(2008, 6, 11);
        Console.WriteLine(dateValue.ToString("ddd", 
                            new CultureInfo("fr-FR")));    
    }
}
// The example displays the following output:
//       mer. 
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#
      Console.WriteLine(dateValue.ToString("ddd", 
                        New CultureInfo("fr-FR")))
   End Sub
End Module
' The example displays the following output:
'       mer.
```

## <a name="to-extract-the-full-weekday-name-from-a-specific-date"></a>Para extrair o nome completo do dia da semana de uma determinada data

1. Se você estiver trabalhando com a representação de cadeia de caracteres de uma data, converta-a para um valor [DateTime](xref:System.DateTime) ou [DateTimeOffset](xref:System.DateTimeOffset) usando o método estático [DateTime.Parse](xref:System.DateTime.Parse(System.String)) ou [DateTimeOffset.Parse](xref:System.DateTimeOffset.Parse(System.String)).

2. Você pode extrair o nome de dia da semana abreviado da cultura atual ou de uma cultura específica:

    a. Para extrair o nome de dia da semana abreviado da cultura atual, chame o método de instância [DateTime.ToString(String)](xref:System.DateTimeSystem.DateTime.ToString(System.String) ou [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) dos valores de data e hora e apresente a cadeia de caracteres "dddd" como o parâmetro *format*. O exemplo a seguir ilustra a chamada para o método `ToString(String)`.

```csharp
using System;

public class Example
{
    public static void Main()
    {
        DateTime dateValue = new DateTime(2008, 6, 11);
        Console.WriteLine(dateValue.ToString("dddd"));    
    }
}
// The example displays the following output:
//       Wednesday
```

```vb
Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#
      Console.WriteLine(dateValue.ToString("dddd"))
   End Sub
End Module
' The example displays the following output:
'       Wednesday
```

    b. To extract the weekday name for a specific culture, call the date and time value’s [DateTime.ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) or [DateTimeOffset.ToString(String, IFormatProvider)](xref:System.DateTimeOffset.ToString(System.String,System.IFormatProvider)) instance method. Pass the string "dddd" as the *format* parameter. Pass either a [CultureInfo](xref:System.Globalization.CultureInfo) or a [DateTimeFormatInfo](xref:System.Globalization.DateTimeFormatInfo) object that represents the culture whose weekday name you want to retrieve as the *provider* parameter. The following code illustrates a call to the [ToString(String, IFormatProvider)](xref:System.DateTime.ToString(System.String,System.IFormatProvider)) method using a [CultureInfo](xref:System.Globalization.CultureInfo) object that represents the es-ES  culture.

```csharp
using System;
using System.Globalization;

public class Example
{
    public static void Main()
    {
        DateTime dateValue = new DateTime(2008, 6, 11);
        Console.WriteLine(dateValue.ToString("dddd", 
                            new CultureInfo("es-ES")));    
    }
}
// The example displays the following output:
//       miércoles.
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#
      Console.WriteLine(dateValue.ToString("dddd", _
                        New CultureInfo("es-ES"))) 
   End Sub
End Module
' The example displays the following output:
'       miércoles.
```

## <a name="example"></a>Exemplo

O exemplo ilustra chamadas para as propriedades [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) e [DateTimeOffset.DayOfWeek](xref:System.DateTimeOffset.DayOfWeek) e os métodos [DateTime.ToString(String)](xref:System.DateTime.ToString(System.String) ou [DateTimeOffset.ToString(String)](xref:System.DateTimeOffset.ToString(System.String)) para recuperar o número que representa o dia da semana, o nome do dia da semana abreviado e o nome completo do dia da semana para uma determinada data. 

```csharp
using System;
using System.Globalization;

public class Example
{
   public static void Main()
   {
      string dateString = "6/11/2007";
      DateTime dateValue;
      DateTimeOffset dateOffsetValue;

      try
      {
         DateTimeFormatInfo dateTimeFormats;
         // Convert date representation to a date value
         dateValue = DateTime.Parse(dateString, CultureInfo.InvariantCulture);
         dateOffsetValue = new DateTimeOffset(dateValue, 
                                      TimeZoneInfo.Local.GetUtcOffset(dateValue));         

         // Convert date representation to a number indicating the day of week
         Console.WriteLine((int) dateValue.DayOfWeek);
         Console.WriteLine((int) dateOffsetValue.DayOfWeek);

         // Display abbreviated weekday name using current culture
         Console.WriteLine(dateValue.ToString("ddd"));
         Console.WriteLine(dateOffsetValue.ToString("ddd"));

         // Display full weekday name using current culture
         Console.WriteLine(dateValue.ToString("dddd"));
         Console.WriteLine(dateOffsetValue.ToString("dddd"));

         // Display abbreviated weekday name for de-DE culture
         Console.WriteLine(dateValue.ToString("ddd", new CultureInfo("de-DE")));
         Console.WriteLine(dateOffsetValue.ToString("ddd", 
                                                     new CultureInfo("de-DE")));

         // Display abbreviated weekday name with de-DE DateTimeFormatInfo object
         dateTimeFormats = new CultureInfo("de-DE").DateTimeFormat;
         Console.WriteLine(dateValue.ToString("ddd", dateTimeFormats));
         Console.WriteLine(dateOffsetValue.ToString("ddd", dateTimeFormats));

         // Display full weekday name for fr-FR culture
         Console.WriteLine(dateValue.ToString("ddd", new CultureInfo("fr-FR")));
         Console.WriteLine(dateOffsetValue.ToString("ddd", 
                                                    new CultureInfo("fr-FR")));

         // Display abbreviated weekday name with fr-FR DateTimeFormatInfo object
         dateTimeFormats = new CultureInfo("fr-FR").DateTimeFormat;
         Console.WriteLine(dateValue.ToString("dddd", dateTimeFormats));
         Console.WriteLine(dateOffsetValue.ToString("dddd", dateTimeFormats));
      }
      catch (FormatException)
      {
         Console.WriteLine("Unable to convert {0} to a date.", dateString);
      }
   }
}
// The example displays the following output:
//       1
//       1
//       Mon
//       Mon
//       Monday
//       Monday
//       Mo
//       Mo
//       Mo
//       Mo
//       lun.
//       lun.
//       lundi
//       lundi
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateString As String = "6/11/2007"
      Dim dateValue As Date
      Dim dateOffsetValue As DateTimeOffset

      Try
         Dim dateTimeFormats As DateTimeFormatInfo
         ' Convert date representation to a date value
         dateValue = Date.Parse(dateString, CultureInfo.InvariantCulture)
         dateOffsetValue = New DateTimeOffset(dateValue, _
                                     TimeZoneInfo.Local.GetUtcOffset(dateValue))            
         ' Convert date representation to a number indicating the day of week
         Console.WriteLine(dateValue.DayOfWeek)
         Console.WriteLine(dateOffsetValue.DayOfWeek)

         ' Display abbreviated weekday name using current culture
         Console.WriteLine(dateValue.ToString("ddd"))
         Console.WriteLine(dateOffsetValue.ToString("ddd"))

         ' Display full weekday name using current culture
         Console.WriteLine(dateValue.ToString("dddd"))
         Console.WriteLine(dateOffsetValue.ToString("dddd"))

         ' Display abbreviated weekday name for de-DE culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("de-DE")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("de-DE")))

         ' Display abbreviated weekday name with de-DE DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("de-DE").DateTimeFormat
         Console.WriteLine(dateValue.ToString("ddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("ddd", dateTimeFormats))

         ' Display full weekday name for fr-FR culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("fr-FR")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("fr-FR")))

         ' Display abbreviated weekday name with fr-FR DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("fr-FR").DateTimeFormat
         Console.WriteLine(dateValue.ToString("dddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("dddd", dateTimeFormats))
      Catch e As FormatException
         Console.WriteLine("Unable to convert {0} to a date.", dateString)
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'       1
'       1
'       Mon
'       Mon
'       Monday
'       Monday
'       Mo
'       Mo
'       Mo
'       Mo
'       lun.
'       lun.
'       lundi
'       lundi
```

Cada linguagem pode contar com funcionalidades que duplicam ou complementam a funcionalidade oferecida pelo .NET. Por exemplo, o Visual Basic tem duas funções desse tipo:

* `Weekday`, que retorna um número que indica o dia da semana de uma determinada data. Ele leva em consideração que o primeiro dia da semana tem valor ordinal um, enquanto a propriedade [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) considera o valor ordinal desse dia como zero.

* `WeekdayName`, que retorna o nome da semana na cultura atual e que corresponde ao número de um determinado dia da semana.

O exemplo a seguir ilustra o uso das funções `Weekday` e `WeekdayName` do Visual Basic.

```vb
Imports System.Globalization
Imports System.Threading

Module Example
   Public Sub Main()
      Dim dateValue As Date = #6/11/2008#

      ' Get weekday number using Visual Basic Weekday function
      Console.WriteLine(Weekday(dateValue))                 ' Displays 4
      ' Compare with .NET DateTime.DayOfWeek property
      Console.WriteLine(dateValue.DayOfWeek)                ' Displays 3

      ' Get weekday name using Weekday and WeekdayName functions
      Console.WriteLine(WeekdayName(Weekday(dateValue)))    ' Displays Wednesday

      ' Change culture to de-DE
      Dim originalCulture As CultureInfo = Thread.CurrentThread.CurrentCulture
      Thread.CurrentThread.CurrentCulture = New CultureInfo("de-DE")
      ' Get weekday name using Weekday and WeekdayName functions
      Console.WriteLine(WeekdayName(Weekday(dateValue)))   ' Displays Donnerstag

      ' Restore original culture
      Thread.CurrentThread.CurrentCulture = originalCulture   
   End Sub
End Module
``` 

Você também pode usar o valor retornado pela propriedade [Datetime.DayOfWeek](xref:System.DateTime.DayOfWeek) para recuperar o nome de dia da semana de uma determinada data. Isso requer apenas uma chamada ao método [Enum.ToString](xref:System.Enum.ToString(System.String)) no valor [DayOfWeek](xref:System.DayOfWeek) retornado pela propriedade. No entanto, essa técnica não gera um nome de dia da semana localizado para a cultura atual, como mostra o exemplo a seguir. 

```csharp
using System;
using System.Globalization;
using System.Threading;

public class Example
{
   public static void Main()
   {
      // Change current culture to fr-FR
      CultureInfo originalCulture = Thread.CurrentThread.CurrentCulture;
      Thread.CurrentThread.CurrentCulture = new CultureInfo("fr-FR");

      DateTime dateValue = new DateTime(2008, 6, 11);
      // Display the DayOfWeek string representation
      Console.WriteLine(dateValue.DayOfWeek.ToString());   
      // Restore original current culture
      Thread.CurrentThread.CurrentCulture = originalCulture;
   }
}
// The example displays the following output:
//       Wednesday
```

```vb
Imports System.Globalization

Module Example
   Public Sub Main()
      Dim dateString As String = "6/11/2007"
      Dim dateValue As Date
      Dim dateOffsetValue As DateTimeOffset

      Try
         Dim dateTimeFormats As DateTimeFormatInfo
         ' Convert date representation to a date value
         dateValue = Date.Parse(dateString, CultureInfo.InvariantCulture)
         dateOffsetValue = New DateTimeOffset(dateValue, _
                                     TimeZoneInfo.Local.GetUtcOffset(dateValue))            
         ' Convert date representation to a number indicating the day of week
         Console.WriteLine(dateValue.DayOfWeek)
         Console.WriteLine(dateOffsetValue.DayOfWeek)

         ' Display abbreviated weekday name using current culture
         Console.WriteLine(dateValue.ToString("ddd"))
         Console.WriteLine(dateOffsetValue.ToString("ddd"))

         ' Display full weekday name using current culture
         Console.WriteLine(dateValue.ToString("dddd"))
         Console.WriteLine(dateOffsetValue.ToString("dddd"))

         ' Display abbreviated weekday name for de-DE culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("de-DE")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("de-DE")))

         ' Display abbreviated weekday name with de-DE DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("de-DE").DateTimeFormat
         Console.WriteLine(dateValue.ToString("ddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("ddd", dateTimeFormats))

         ' Display full weekday name for fr-FR culture
         Console.WriteLine(dateValue.ToString("ddd", New CultureInfo("fr-FR")))
         Console.WriteLine(dateOffsetValue.ToString("ddd", _
                                                    New CultureInfo("fr-FR")))

         ' Display abbreviated weekday name with fr-FR DateTimeFormatInfo object
         dateTimeFormats = New CultureInfo("fr-FR").DateTimeFormat
         Console.WriteLine(dateValue.ToString("dddd", dateTimeFormats))
         Console.WriteLine(dateOffsetValue.ToString("dddd", dateTimeFormats))
      Catch e As FormatException
         Console.WriteLine("Unable to convert {0} to a date.", dateString)
      End Try
   End Sub
End Module
' The example displays the following output to the console:
'       1
'       1
'       Mon
'       Mon
'       Monday
'       Monday
'       Mo
'       Mo
'       Mo
'       Mo
'       lun.
'       lun.
'       lundi
'       lundi
```

## <a name="see-also"></a>Consulte também

[Executando operações de formatação](performing-formatting-operations.md)

[Cadeias de caracteres de formato de data e hora padrão](standard-datetime.md)

[Cadeias de caracteres de formato de data e hora personalizado](custom-datetime.md)
    

