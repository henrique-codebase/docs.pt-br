---
title: TRATAR (Entity SQL)
ms.date: 03/30/2017
ms.assetid: 5b77f156-55de-4cb4-8154-87f707d4c635
ms.openlocfilehash: 06c4200434f443446e8981dcefe2baf43b1af4b0
ms.sourcegitcommit: 7588136e355e10cbc2582f389c90c127363c02a5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/12/2020
ms.locfileid: "79149889"
---
# <a name="treat-entity-sql"></a>TRATAR (Entity SQL)
Trata um objeto de um tipo base específico como um objeto do tipo derivado especificado.  
  
## <a name="syntax"></a>Sintaxe  
  
```sql  
TREAT ( expression as type)  
```  
  
## <a name="arguments"></a>Argumentos  
 `expression`  
 Qualquer expressão de consulta válida que retorna uma entidade.  
  
> [!NOTE]
> O tipo da expressão especificada deve ser um subtipo do tipo de dados especificado, ou o tipo de dados deve ser um subtipo do tipo da expressão.  
  
 `type`  
 Um tipo de objeto. O tipo deve ser qualificado por um namespace.  
  
> [!NOTE]
> A expressão especificada deve ser um subtipo do tipo de dados especificado, ou o tipo de dados deve ser um subtipo da expressão.  
  
## <a name="return-value"></a>Valor retornado  
 Um valor de tipo de dados especificado.  
  
## <a name="remarks"></a>Comentários  
 O DELEITE é usado para executar upcasting entre classes relacionadas. Por exemplo, se `Employee` deriva de `Person` e p é do tipo `Person`, upcasts de `TREAT(p AS NamespaceName.Employee)` uma instância genérica de `Person` a `Employee`; isto é, permite que você trate p como `Employee`.  
  
 O DELEITE é usado em cenários de herança onde você pode fazer uma consulta como o seguinte:  
  
```sql  
SELECT TREAT(p AS NamespaceName.Employee)  
FROM ContainerName.Person AS p  
WHERE p IS OF (NamespaceName.Employee)
```  
  
 As entidades de `Person` de upcasts desta consulta a `Employee` tipo. Se o valor de p verdade não é do tipo `Employee`, a expressão produz o valor `null`.  
  
> [!NOTE]
> A expressão `Employee` especificada deve ser um subtipo `Person`do tipo de dados especificado, ou o tipo de dados deve ser um subtipo da expressão. Caso contrário, a expressão resultará em um erro em tempo de compilação.  
  
 A tabela a seguir mostra o comportamento de tratam sobre alguns padrões típicos e alguns padrões menos comuns. Todas as exceções são geradas do lado do cliente antes que o provedor obtenha chamado:  
  
|Padrão|Comportamento|  
|-------------|--------------|  
|`TREAT (null AS EntityType)`|Retorna `DbNull`.|  
|`TREAT (null AS ComplexType)`|Gerencie uma exceção.|  
|`TREAT (null AS RowType)`|Gerencie uma exceção|  
|`TREAT (EntityType AS EntityType)`|Retorna `EntityType` ou `null`.|  
|`TREAT (ComplexType AS ComplexType)`|Gerencie uma exceção.|  
|`TREAT (RowType AS RowType)`|Gerencie uma exceção.|  
  
## <a name="example"></a>Exemplo  
 A seguinte consulta de [!INCLUDE[esql](../../../../../../includes/esql-md.md)] usa o operador de DELEITE para converter um objeto do traço de tipo a uma coleção de objetos do tipo OnsiteCourse. A consulta é baseada no [Modelo Escolar](https://docs.microsoft.com/previous-versions/dotnet/netframework-4.0/bb896300(v=vs.100)).  
  
 [!code-sql[DP EntityServices Concepts#TREAT_ISOF](~/samples/snippets/tsql/VS_Snippets_Data/dp entityservices concepts/tsql/entitysql.sql#treat_isof)]  
  
## <a name="see-also"></a>Confira também

- [Referência de Entity SQL](entity-sql-reference.md)
- [Tipos estruturados que permitem valor nulo](nullable-structured-types-entity-sql.md)
