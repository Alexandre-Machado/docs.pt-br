---
title: "Como criar um novo método para uma enumeração (Guia de Programação em C#) | Microsoft Docs"
ms.date: 2015-07-20
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
dev_langs:
- CSharp
helpviewer_keywords:
- enumerations [C#]
- extension methods [C#], for enums
- enum extensibility [C#]
ms.assetid: 100106f9-1e54-462c-8ebe-3892fe23b6eb
caps.latest.revision: 7
author: BillWagner
ms.author: wiwagn
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Human Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 3d15cbcdd81584ea5c6ab40d231183f883a7a805
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-create-a-new-method-for-an-enumeration-c-programming-guide"></a>Como criar um novo método para uma enumeração (Guia de Programação em C#)
Você pode usar métodos de extensão para adicionar funcionalidades específica para um tipo de enumeração específico.  
  
## <a name="example"></a>Exemplo  
 No exemplo a seguir, a enumeração `Grades` representa as letras possíveis que um aluno pode receber em uma classe. Um método de extensão chamado `Passing` é adicionado ao tipo `Grades` de forma que cada instância desse tipo agora "sabe" se ele representa uma nota de aprovação ou não.  
  
 [!code-cs[csProgGuideExtensionMethods#2](../../../csharp/programming-guide/classes-and-structs/codesnippet/CSharp/how-to-create-a-new-method-for-an-enumeration_1.cs)]  
  
 Observe que a classe `Extensions` também contém uma variável estática atualizada dinamicamente e que o valor retornado do método de extensão reflete o valor atual dessa variável. Isso demonstra que, nos bastidores, os métodos de extensão são chamados diretamente na classe estática na qual eles são definidos.  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Para executar esse código, copie e cole-o em um console de projeto de aplicativo do Visual C# que foi criado no [!INCLUDE[vs_current_short](../../../csharp/programming-guide/classes-and-structs/includes/vs_current_short_md.md)]. Por padrão, esse projeto é direcionado para a versão 3.5 do [!INCLUDE[dnprdnshort](../../../csharp/getting-started/includes/dnprdnshort_md.md)] e ele tem uma referência ao System.Core.dll e uma diretriz `using` para System.Linq. Se um ou mais desses requisitos estiverem ausentes no projeto, você poderá adicioná-los manualmente.   
  
## <a name="see-also"></a>Consulte também  
 [Guia de Programação em C#](../../../csharp/programming-guide/index.md)   
 [Métodos de Extensão](../../../csharp/programming-guide/classes-and-structs/extension-methods.md)
