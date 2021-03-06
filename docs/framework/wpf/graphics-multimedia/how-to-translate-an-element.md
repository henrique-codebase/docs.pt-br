---
title: Como converter um elemento
ms.date: 03/30/2017
helpviewer_keywords:
- graphics [WPF], translations
ms.assetid: 461c8273-15df-42f6-8672-89ba22887cc0
ms.openlocfilehash: addff0e22fb3f27ea924887809c0635aeb3ad67d
ms.sourcegitcommit: 267d092663aba36b6b2ea853034470aea493bfae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/21/2020
ms.locfileid: "80111966"
---
# <a name="how-to-translate-an-element"></a>Como converter um elemento
Este exemplo mostra como traduzir (mover) <xref:System.Windows.Media.TranslateTransform>um elemento usando um .  
  
 A <xref:System.Windows.Media.TranslateTransform> classe é especialmente útil para mover elementos dentro de painéis que não suportam posicionamento absoluto. Por exemplo, aplicando <xref:System.Windows.Media.TranslateTransform> um <xref:System.Windows.UIElement.RenderTransform%2A> à propriedade de um elemento, <xref:System.Windows.Controls.StackPanel> você <xref:System.Windows.Controls.DockPanel>pode mover um elemento dentro de um ou .  
  
 Use <xref:System.Windows.Media.TranslateTransform.X%2A> a propriedade <xref:System.Windows.Media.TranslateTransform> do para especificar a quantidade, em pixels, para mover o elemento ao longo do eixo x. Use <xref:System.Windows.Media.TranslateTransform.Y%2A> a propriedade para especificar a quantidade, em pixels, para mover o elemento ao longo do eixo y. Por fim, <xref:System.Windows.Media.TranslateTransform> aplique <xref:System.Windows.UIElement.RenderTransform%2A> a propriedade do elemento.  
  
 O exemplo a <xref:System.Windows.Media.TranslateTransform> seguir usa um para mover um elemento 50 pixels para a direita e 50 pixels para baixo.  
  
## <a name="example"></a>Exemplo  
 [!code-xaml[transformsSample#53](~/samples/snippets/csharp/VS_Snippets_Wpf/transformsSample/CS/TranslateTransformExample.xaml#53)]  
  
 Para obter a amostra completa, consulte [2D Transforms Sample](https://github.com/Microsoft/WPF-Samples/tree/master/Graphics/2DTransforms).  
  
## <a name="see-also"></a>Confira também

- [Visão geral de transformações](transforms-overview.md)
