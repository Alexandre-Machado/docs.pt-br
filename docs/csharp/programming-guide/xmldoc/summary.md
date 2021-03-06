---
title: "&lt;summary&gt; (Guia de Programação em C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
f1_keywords:
- <summary>
- summary
dev_langs:
- CSharp
helpviewer_keywords:
- <summary> C# XML tag
- summary C# XML tag
ms.assetid: b4c43d92-2067-4eac-a59a-d32f5248c08b
caps.latest.revision: 17
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
ms.translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: b74e5bf964ff82f88fe2822257a64eccb5697535
ms.contentlocale: pt-br
ms.lasthandoff: 03/13/2017

---
# <a name="ltsummarygt-c-programming-guide"></a>&lt;summary&gt; (Guia de Programação em C#)
## <a name="syntax"></a>Sintaxe  
  
```  
<summary>description</summary>  
```  
  
#### <a name="parameters"></a>Parâmetros  
 `description`  
 Um resumo do objeto.  
  
## <a name="remarks"></a>Comentários  
 A marca \<summary> deve ser usada para descrever um tipo ou um membro de tipo. Use [\<remarks>](../../../csharp/programming-guide/xmldoc/remarks.md) para adicionar mais informações a uma descrição de tipo. Use o [atributo cref](../../../csharp/programming-guide/xmldoc/cref-attribute.md) para habilitar ferramentas de documentação como [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061) a criarem hiperlinks internos para páginas de documentação para elementos de código.  
  
 O texto da marca \<summary> é a única fonte de informações sobre o tipo no IntelliSense e também é exibido na janela Pesquisador de Objetos.  
  
 Compile com [/doc](../../../csharp/language-reference/compiler-options/doc-compiler-option.md) para processar comentários de documentação em um arquivo. Para criar a documentação final baseada no arquivo gerado pelo compilador, você pode criar uma ferramenta personalizada ou usar uma ferramenta como o [Sandcastle](http://go.microsoft.com/fwlink/?LinkId=124061).  
  
## <a name="example"></a>Exemplo  
 [!code-cs[csProgGuideDocComments#12](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_1.cs)]  
  
 O exemplo anterior produz o seguinte arquivo XML.  
  
```  
<?xml version="1.0"?>  
<doc>  
    <assembly>  
        <name>YourNamespace</name>  
    </assembly>  
    <members>  
        <member name="T:DotNetEvents.TestClass">  
            text for class TestClass  
        </member>  
        <member name="M:DotNetEvents.TestClass.DoWork(System.Int32)">  
            <summary>DoWork is a method in the TestClass class.  
            <para>Here's how you could make a second paragraph in a description. <see cref="M:System.Console.WriteLine(System.String)"/> for information about output statements.</para>  
            <seealso cref="M:DotNetEvents.TestClass.Main"/>  
            </summary>  
        </member>  
        <member name="M:DotNetEvents.TestClass.Main">  
            text for Main  
        </member>  
    </members>  
</doc>  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como fazer uma referência `cref` para um tipo genérico.  
  
 [!code-cs[csProgGuideDocComments#11](../../../csharp/programming-guide/xmldoc/codesnippet/CSharp/summary_2.cs)]  
  
 O exemplo anterior produz o seguinte arquivo XML.  
  
```  
<?xml version="1.0"?>  
<doc>  
    <assembly>  
        <name>YourNamespace</name>  
    </assembly>  
    <members>  
        <member name="T:ExtensionMethodsDemo1.A">  
            <summary cref="T:ExtensionMethodsDemo1.C`1">  
            </summary>  
        </member>  
        <member name="T:ExtensionMethodsDemo1.B">  
            <summary cref="T:C`1">  
            </summary>  
        </member>  
        <member name="T:ExtensionMethodsDemo1.C`1">  
            <summary cref="T:ExtensionMethodsDemo1.A">  
            </summary>  
            <typeparam name="T"></typeparam>  
        </member>  
    </members>  
</doc>  
```  
  
## <a name="see-also"></a>Consulte também  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)   
 [Marcas recomendadas para comentários de documentação](../../../csharp/programming-guide/xmldoc/recommended-tags-for-documentation-comments.md)

