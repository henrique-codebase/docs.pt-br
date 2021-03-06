---
title: Ativar exibição de azulejo no controle listView
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
- cpp
helpviewer_keywords:
- tile view feature
- tiling
- Windows Forms, controls
- ListView control [Windows Forms], tile view
ms.assetid: c20e67a3-2d94-413d-9fcf-ecbd0fe251da
ms.openlocfilehash: 1478ba5e4f175cd7d9ec7ab5c3c4bc9050ce02fb
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79182159"
---
# <a name="how-to-enable-tile-view-in-a-windows-forms-listview-control"></a>Como habilitar exibição lado a lado em um controle ListView dos Windows Forms
Com o recurso de <xref:System.Windows.Forms.ListView> exibição de ladrilhos do controle, você pode fornecer um equilíbrio visual entre informações gráficas e texais. As informações textuais exibidas para um item na exibição lado a lado são as mesmas que as informações de coluna definidas para exibição de detalhes. A exibição de azulejo funciona em combinação <xref:System.Windows.Forms.ListView> com os recursos de marca de agrupamento ou de inserção no controle.  
  
 O modo de exibição lado a lado usa um ícone de 32 x 32 pixels e várias linhas de texto, conforme mostrado nas imagens a seguir.  
  
 ![Exibição lado a lado em um controle ListView](./media/how-to-enable-tile-view-in-a-windows-forms-listview-control/tile-view-in-listview-control.gif "Ícones e texto da exibição lado a lado")  

 Para habilitar a <xref:System.Windows.Forms.ListView.View%2A> visualização <xref:System.Windows.Forms.View.Tile>de azulejos, defina a propriedade como . Você pode ajustar o tamanho das <xref:System.Windows.Forms.ListView.TileSize%2A> telhas definindo a propriedade e o número <xref:System.Windows.Forms.ListView.Columns%2A> de linhas de texto exibidas no azulejo, ajustando a coleção.  
  
### <a name="to-set-tile-view-programmatically"></a>Para definir a exibição lado a lado programaticamente  
  
1. Use <xref:System.Windows.Forms.View> a enumeração <xref:System.Windows.Forms.ListView> do controle.  
  
    ```vb  
    ListView1.View = View.Tile  
    ```  
  
    ```csharp  
    listView1.View = View.Tile;  
    ```  
  
## <a name="example"></a>Exemplo  
 O exemplo de código completo a seguir demonstra a exibição lado a lado com blocos modificados para mostrar as três linhas de texto. O tamanho de bloco foi ajustado para evitar encapsulamento de linha.  
  
 [!code-cpp[System.Windows.Forms.ListView.Tiling#1](~/samples/snippets/cpp/VS_Snippets_Winforms/System.Windows.Forms.ListView.Tiling/CPP/listviewtilingexample.cpp#1)]
 [!code-csharp[System.Windows.Forms.ListView.Tiling#1](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Windows.Forms.ListView.Tiling/CS/listviewtilingexample.cs#1)]
 [!code-vb[System.Windows.Forms.ListView.Tiling#1](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Windows.Forms.ListView.Tiling/VB/listviewtilingexample.vb#1)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 Este exemplo requer:  
  
- Referências aos assemblies System e System.Windows.Forms.  
  
- Um arquivo de ícone denominado book.ico no mesmo diretório do arquivo executável.  
  
## <a name="see-also"></a>Confira também

- <xref:System.Windows.Forms.ListView>
- <xref:System.Windows.Forms.ListView.TileSize%2A>
- [Controle ListView](listview-control-windows-forms.md)
- [Visão geral do controle ListView](listview-control-overview-windows-forms.md)
