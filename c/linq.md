# LINQ

## 基本查询操作 <a id="basic-linq-query-operations-c"></a>

### 筛选 <a id="filtering"></a>

或许，最常见的查询操作是以布尔表达式的形式应用筛选器。 筛选器使查询仅返回表达式为 true 的元素。 将通过使用 `where` 子句生成结果。 筛选器实际指定要从源序列排除哪些元素。 在下列示例中，仅返回地址位于“London”的 `customers`。

```csharp
var queryLondonCustomers = from cust in customers
                           where cust.City == "London"
                           select cust;
```

可使用熟悉的 C\# 逻辑 `AND` 和 `OR` 运算符，在 `where` 子句中根据需要应用尽可能多的筛选器表达式。 例如，若要仅返回来自“London”的客户 `AND` 该客户名称为“Devon”，可编写以下代码：C\#

```csharp
where cust.City=="London" && cust.Name == "Devon"
```

要返回来自 London 或 Paris 的客户，可编写以下代码：C\#

```csharp
where cust.City == "London" || cust.City == "Paris"
```

有关详细信息，请参阅 [where 子句](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/where-clause)。

### 中间件排序 <a id="ordering"></a>

对返回的数据进行排序通常很方便。 `orderby` 子句根据要排序类型的默认比较器，对返回序列中的元素排序。 例如，基于 `Name` 属性，可将下列查询扩展为对结果排序。 由于 `Name` 是字符串，默认比较器将按字母顺序从 A 到 Z 进行排序。C\#

```csharp
var queryLondonCustomers3 = 
    from cust in customers
    where cust.City == "London"
    orderby cust.Name ascending
    select cust;
```

要对结果进行从 Z 到 A 的逆序排序，请使用 `orderby…descending` 子句。

有关详细信息，请参阅 [orderby 子句](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/orderby-clause)。

### 分组 <a id="grouping"></a>

`group` 子句用于对根据您指定的键所获得的结果进行分组。 例如，可指定按 `City` 对结果进行分组，使来自 London 或 Paris 的所有客户位于单独的组内。 在这种情况下，`cust.City` 是键。C\#

```csharp
// queryCustomersByCity is an IEnumerable<IGrouping<string, Customer>>
  var queryCustomersByCity =
      from cust in customers
      group cust by cust.City;

  // customerGroup is an IGrouping<string, Customer>
  foreach (var customerGroup in queryCustomersByCity)
  {
      Console.WriteLine(customerGroup.Key);
      foreach (Customer customer in customerGroup)
      {
          Console.WriteLine("    {0}", customer.Name);
      }
  }
```

使用 `group` 子句结束查询时，结果将以列表的形式列出。 列表中的每个元素都是具有 `Key` 成员的对象，列表中的元素根据该键被分组。 在循环访问生成组序列的查询时，必须使用嵌套 `foreach` 循环。 外层循环循环访问每个组，内层循环循环访问每个组的成员。

如果必须引用某个组操作的结果，可使用 `into` 关键字创建能被进一步查询的标识符。 下列查询仅返回包含两个以上客户的组：C\#

```csharp
// custQuery is an IEnumerable<IGrouping<string, Customer>>
var custQuery =
    from cust in customers
    group cust by cust.City into custGroup
    where custGroup.Count() > 2
    orderby custGroup.Key
    select custGroup;
```

有关详细信息，请参阅 [group 子句](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/group-clause)。

### 联接 <a id="joining"></a>

联接操作在不同序列间创建关联，这些序列在数据源中未被显式模块化。 例如，可通过执行联接来查找所有位置相同的客户和分销商。 在 LINQ 中，`join` 子句始终作用于对象集合，而非直接作用于数据库表。C\#

```csharp
var innerJoinQuery =
    from cust in customers
    join dist in distributors on cust.City equals dist.City
    select new { CustomerName = cust.Name, DistributorName = dist.Name };
```

在 LINQ 中，不必像在 SQL 中那样频繁使用 `join`，因为 LINQ 中的外键在对象模型中表示为包含项集合的属性。 例如 `Customer` 对象包含 `Order` 对象的集合。 不必执行联接，只需使用点表示法访问订单：C\#

```csharp
from order in Customer.Orders...  
```

有关详细信息，请参阅 [join 子句](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/join-clause)。

### 选择（投影） <a id="selecting-projections"></a>

`select` 子句生成查询结果并指定每个返回的元素的“形状”或类型。 例如，可以指定结果包含的是整个 `Customer` 对象、仅一个成员、成员的子集，还是某个基于计算或新对象创建的完全不同的结果类型。 当 `select` 子句生成除源元素副本以外的内容时，该操作称为投影。 使用投影转换数据是 LINQ 查询表达式的一种强大功能。 有关详细信息，请参阅[使用 LINQ \(C\#\)](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/linq/data-transformations-with-linq) 和 [select 子句](https://docs.microsoft.com/zh-cn/dotnet/csharp/language-reference/keywords/select-clause)进行数据转换。

## Ref

[语言集成查询 \(LINQ\) \(C\#\) \| Microsoft Docs](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/linq/)

[LINQ 中的查询语法和方法语法 \(C\#\) \| Microsoft Docs](https://docs.microsoft.com/zh-cn/dotnet/csharp/programming-guide/concepts/linq/query-syntax-and-method-syntax-in-linq)

