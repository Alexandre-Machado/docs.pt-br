---
title: Atributos (C#) | Microsoft Docs
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
ms.assetid: f148f13f-a0d5-4f22-9c87-4b73d5dde270
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e793ac7647c63125bf7bf075cdba57e770cc3be4
ms.lasthandoff: 03/13/2017

---
# <a name="attributes-c"></a>Atributos (C#)
Os atributos fornecem um método eficiente de associação de metadados, ou informações declarativas, ao código (assemblies, tipos, métodos, propriedades e etc.). Após um atributo ser associado a uma entidade de programa, o atributo poderá ser consultado no tempo de execução usando uma técnica chamada *reflexão*. Para obter mais informações, consulte [Reflexão (C#)](../../../../csharp/programming-guide/concepts/reflection.md).  
  
 Os atributos têm as seguintes propriedades:  
  
-   Os atributos adicionam metadados ao seu programa. Os *metadados* são informações sobre os tipos definidos em um programa. Todos os assemblies .NET contêm um conjunto de metadados especificado que descreve os tipos e os membros de tipo definidos no assembly. Você pode adicionar atributos personalizados para especificar qualquer informação adicional necessária. Para obter mais informações, consulte [Criando atributos personalizados (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md).  
  
-   Você pode aplicar um ou mais atributos a assemblies completos, módulos ou elementos de programas menores, como classes e propriedades.  
  
-   Os atributos podem aceitar argumentos da mesma forma que métodos e propriedades.  
  
-   Seu programa pode examinar seus próprios metadados ou os metadados em outros programas usando reflexão. Para obter mais informações, consulte [Acessando atributos usando reflexão (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md).  
  
## <a name="using-attributes"></a>Usando atributos  
 Os atributos podem ser colocados em quase qualquer declaração, embora um atributo específico possa restringir os tipos de declarações nas quais ele é válido. No C#, você especifica um atributo colocando o nome do atributo entre colchetes ([]) acima da declaração da entidade à qual ele se aplica.  
  
 Neste exemplo, o atributo <xref:System.SerializableAttribute> é usado para aplicar uma característica específica a uma classe:  
  
```csharp  
[System.Serializable]  
public class SampleClass  
{  
    // Objects of this type can be serialized.  
}  
```  
  
 Um método com o atributo <xref:System.Runtime.InteropServices.DllImportAttribute> é declarado do seguinte modo:  
  
```csharp  
using System.Runtime.InteropServices;  
```  
  
```csharp  
[System.Runtime.InteropServices.DllImport("user32.dll")]  
extern static void SampleMethod();  
```  
  
 Mais de um atributo pode ser colocado em uma declaração:  
  
```csharp  
using System.Runtime.InteropServices;  
```  
  
```csharp  
void MethodA([In][Out] ref double x) { }  
void MethodB([Out][In] ref double x) { }  
void MethodC([In, Out] ref double x) { }  
```  
  
 Alguns atributos podem ser especificados mais de uma vez para uma determinada entidade. Um exemplo de tal atributo de múltiplos usos é <xref:System.Diagnostics.ConditionalAttribute>:  
  
```csharp  
[Conditional("DEBUG"), Conditional("TEST1")]  
void TraceMethod()  
{  
    // ...  
}  
```  
  
> [!NOTE]
>  Por convenção, todos os nomes de atributo terminam com a palavra "Atributo" para distingui-los de outros itens no .NET Framework. No entanto, você não precisa especificar o sufixo de atributo ao usar atributos no código. Por exemplo, `[DllImport]` é equivalente a `[DllImportAttribute]`, mas `DllImportAttribute` é o nome do atributo real no .NET Framework.  
  
### <a name="attribute-parameters"></a>Parâmetros de atributo  
 Muitos atributos têm parâmetros, que podem ser nomeados, sem nome ou posicionais. Quaisquer parâmetros posicionais devem ser especificados em uma determinada ordem e não podem ser omitidos. Os parâmetros nomeados são opcionais e podem ser especificados em qualquer ordem. Os parâmetros posicionais são especificados primeiro. Por exemplo, esses três atributos são equivalentes:  
  
```csharp  
[DllImport("user32.dll")]  
[DllImport("user32.dll", SetLastError=false, ExactSpelling=false)]  
[DllImport("user32.dll", ExactSpelling=false, SetLastError=false)]  
```  
  
 O primeiro parâmetro, o nome da DLL, é posicional e sempre vir em primeiro lugar; os outros são nomeados. Nesse caso, ambos os parâmetros nomeados são padronizados como false e, portanto, podem ser omitidos. Consulte a documentação do atributo individual para obter informações sobre valores de parâmetro padrão.  
  
### <a name="attribute-targets"></a>Destinos de Atributos  
 O *destino* de um atributo é a entidade à qual o atributo se aplica. Por exemplo, um atributo pode ser aplicado a uma classe, um método específico ou um assembly inteiro. Por padrão, um atributo aplica-se ao elemento que ele precede. Mas você pode identificar explicitamente, por exemplo, se um atributo é aplicado a um método, ou a seu parâmetro ou a seu valor retornado.  
  
 Para identificar explicitamente um atributo de destino, use a seguinte sintaxe:  
  
```csharp  
[target : attribute-list]  
```  
  
 A lista de possíveis valores `target` é mostrada na tabela a seguir.  
  
|Valor de destino|Aplica-se a|  
|------------------|----------------|  
|`assembly`|Assembly inteiro|  
|`module`|Módulo do assembly atual|  
|`field`|Campo em uma classe ou um struct|  
|`event`|Evento|  
|`method`|Método ou acessadores de propriedade `get` e `set`|  
|`param`|Parâmetros de método ou parâmetros de acessador de propriedade `set`|  
|`property`|Propriedade|  
|`return`|Valor retornado de um método, indexador de propriedade ou acessador de propriedade `get`|  
|`type`|Struct, classe, interface, enum ou delegado|  
  
 O exemplo a seguir mostra como aplicar atributos a módulos e assemblies. Para obter mais informações, consulte [Atributos comuns (C#)](../../../../csharp/programming-guide/concepts/attributes/common-attributes.md).  
  
```csharp  
using System;  
using System.Reflection;  
[assembly: AssemblyTitleAttribute("Production assembly 4")]  
[module: CLSCompliant(true)]  
```  
  
 O exemplo a seguir mostra como aplicar atributos a métodos, parâmetros de método e valores de retorno de método em C#.  
  
```csharp  
// default: applies to method  
[SomeAttr]  
int Method1() { return 0; }  
  
// applies to method  
[method: SomeAttr]  
int Method2() { return 0; }  
  
// applies to return value  
[return: SomeAttr]  
int Method3() { return 0; }  
```  
  
> [!NOTE]
>  Independentemente dos destinos nos quais `SomeAttr` é definido como válido, o destino `return` deve ser especificado, mesmo se `SomeAttr` forem definidos para serem aplicados somente a valores de retorno. Em outras palavras, o compilador não usará as informações de `AttributeUsage` para resolver os destinos de atributos ambíguos. Para obter mais informações, consulte [AttributeUsage (C#)](../../../../csharp/programming-guide/concepts/attributes/attributeusage.md).  
  
## <a name="common-uses-for-attributes"></a>Usos comuns para os atributos  
 A lista a seguir inclui alguns dos usos comuns de atributos no código:  
  
-   Marcar métodos usando o atributo `WebMethod` nos serviços Web para indicar que o método deve ser chamado por meio do protocolo SOAP. Para obter mais informações, consulte <xref:System.Web.Services.WebMethodAttribute>.  
  
-   Descrever como realizar marshaling de parâmetros de método ao interoperar com código nativo. Para obter mais informações, consulte <xref:System.Runtime.InteropServices.MarshalAsAttribute>.  
  
-   Descrever as propriedades COM para classes, métodos e interfaces.  
  
-   Chamar código não gerenciado usando a classe <xref:System.Runtime.InteropServices.DllImportAttribute>.  
  
-   Descrever o assembly em termos de versão, título, descrição ou marca.  
  
-   Descrever quais membros de uma classe serializar para persistência.  
  
-   Descrever como fazer mapeamento entre nós XML e membros de classe para serialização de XML.  
  
-   Descrever os requisitos de segurança para métodos.  
  
-   Especificar as características usadas para impor a segurança.  
  
-   Controlar otimizações pelo compilador JIT (Just-In-Time) para que o código permaneça fácil de depurar.  
  
-   Obter informações sobre o chamador de um método.  
  
## <a name="related-sections"></a>Seções relacionadas  
 Para obter mais informações, consulte:  
  
-   [Criando atributos personalizados (C#)](../../../../csharp/programming-guide/concepts/attributes/creating-custom-attributes.md)  
  
-   [Acessando atributos usando reflexão (C#)](../../../../csharp/programming-guide/concepts/attributes/accessing-attributes-by-using-reflection.md)  
  
-   [Como criar uma união do C/C++ usando atributos (C#)](../../../../csharp/programming-guide/concepts/attributes/how-to-create-a-c-cpp-union-by-using-attributes.md)  
  
-   [Atributos comuns (C#)](../../../../csharp/programming-guide/concepts/attributes/common-attributes.md)  
  
-   [Informações do chamador (C#)](../../../../csharp/programming-guide/concepts/caller-information.md)  
  
## <a name="see-also"></a>Consulte também  
 [Guia de programação em C#](../../../../csharp/programming-guide/index.md)   
 [Reflexão (C#)](../../../../csharp/programming-guide/concepts/reflection.md)   
 [Atributos](https://msdn.microsoft.com/library/5x6cd29c)
