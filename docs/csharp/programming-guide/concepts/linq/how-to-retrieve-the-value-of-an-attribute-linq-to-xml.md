---
title: Como recuperar o valor de um atributo (LINQ to XML) (C#) | Microsoft Docs
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
ms.assetid: 817bbe89-5979-4234-bf0c-46f63692ac8c
caps.latest.revision: 3
author: BillWagner
ms.author: wiwagn
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 687a9d6da80259d41f6ed541cee4c579cdff23d8
ms.lasthandoff: 03/13/2017


---
# <a name="how-to-retrieve-the-value-of-an-attribute-linq-to-xml-c"></a>Como recuperar o valor de um atributo (LINQ to XML) (C#)
Este tópico mostra como obter o valor de atributos. Existem duas maneiras principais: converter um <xref:System.Xml.Linq.XAttribute> no tipo desejado. Em seguida, o operador de conversão explícita converte o conteúdo do elemento ou do atributo no tipo especificado. Como alternativa, você pode usar a propriedade <xref:System.Xml.Linq.XAttribute.Value%2A>. No entanto, a conversão geralmente é a abordagem recomendada. Se você converter o atributo em um tipo anulável, o código será mais simples de criar ao recuperar o valor de um atributo que pode ou não existir. Para obter exemplos dessa técnica, consulte [Como recuperar o valor de um elemento (LINQ to XML) (C#)](../../../../csharp/programming-guide/concepts/linq/how-to-retrieve-the-value-of-an-element-linq-to-xml.md).  
  
## <a name="example"></a>Exemplo  
 Para recuperar o valor de um atributo, basta converter o objeto <xref:System.Xml.Linq.XAttribute> no tipo desejado.  
  
```csharp  
XElement root = new XElement("Root",  
                    new XAttribute("Attr", "abcde")  
                );  
Console.WriteLine(root);  
string str = (string)root.Attribute("Attr");  
Console.WriteLine(str);  
```  
  
 Este exemplo gera a seguinte saída:  
  
```  
<Root Attr="abcde" />  
abcde  
```  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra como recuperar o valor de um atributo em que o atributo está em um namespace. Para obter mais informações, consulte [Trabalhando com namespaces XML (C#)](../../../../csharp/programming-guide/concepts/linq/working-with-xml-namespaces.md).  
  
```csharp  
XNamespace aw = "http://www.adventure-works.com";  
XElement root = new XElement(aw + "Root",  
                    new XAttribute(aw + "Attr", "abcde")  
                );  
string str = (string)root.Attribute(aw + "Attr");  
Console.WriteLine(str);  
```  
  
 Este exemplo gera a seguinte saída:  
  
```  
abcde  
```  
  
## <a name="see-also"></a>Consulte também  
 [Eixos do LINQ to XML (C#)](../../../../csharp/programming-guide/concepts/linq/linq-to-xml-axes.md)
