---
title: 'Como: preencher figuras abertas'
ms.date: 03/30/2017
dev_langs:
- csharp
- vb
helpviewer_keywords:
- open figures [Windows Forms], filling
- figures [Windows Forms], filling
ms.assetid: 5a36b0e4-f1f4-46c0-a85a-22ae98491950
ms.openlocfilehash: 6ecea7d3edb0c3e25fb4e69ff12b88019e530021
ms.sourcegitcommit: b1cfd260928d464d91e20121f9bdba7611c94d71
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2019
ms.locfileid: "67506078"
---
# <a name="how-to-fill-open-figures"></a>Como: preencher figuras abertas
Você pode preencher um caminho passando um <xref:System.Drawing.Drawing2D.GraphicsPath> do objeto para o <xref:System.Drawing.Graphics.FillPath%2A> método. O <xref:System.Drawing.Graphics.FillPath%2A> método preenche o caminho de acordo com o modo de preenchimento (contorno ou alternativo) definido atualmente para o caminho. Se o caminho tiver figuras abertas, ele será preenchido como se essas figuras que foram fechadas. GDI+ fecha uma figura desenhando uma linha reta do ponto final para o ponto de partida.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir cria um caminho que tem uma figura aberta (um arco) e uma figura fechada (uma elipse). O <xref:System.Drawing.Graphics.FillPath%2A> método preenche o caminho de acordo com o modo de preenchimento padrão, que é <xref:System.Drawing.Drawing2D.FillMode.Alternate>.  
  
 A ilustração a seguir mostra a saída do código de exemplo. Observe que o caminho é preenchido (acordo com a <xref:System.Drawing.Drawing2D.FillMode.Alternate>) como se a figura aberta estivesse fechada por uma linha reta do ponto final para o ponto de partida.  
  
 ![Diagrama que mostra a saída do método FillPath](./media/how-to-fill-open-figures/fill-path-alternate-mode.png)  
  
 [!code-csharp[System.Drawing.ConstructingDrawingPaths#11](~/samples/snippets/csharp/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/CS/Class1.cs#11)]
 [!code-vb[System.Drawing.ConstructingDrawingPaths#11](~/samples/snippets/visualbasic/VS_Snippets_Winforms/System.Drawing.ConstructingDrawingPaths/VB/Class1.vb#11)]  
  
## <a name="compiling-the-code"></a>Compilando o código  
 O exemplo anterior foi projetado para uso com o Windows Forms e requer <xref:System.Windows.Forms.PaintEventArgs> `e`, que é um parâmetro do <xref:System.Windows.Forms.Control.Paint> manipulador de eventos.  
  
## <a name="see-also"></a>Consulte também

- <xref:System.Drawing.Drawing2D.GraphicsPath>
- [Caminhos de Elementos Gráficos no GDI+](graphics-paths-in-gdi.md)
