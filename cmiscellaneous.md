# C#Miscellaneous

## List 传值复制

- ToArray()

```
List<string> t = new List<string>(); //original
List<string> t2 = new List<string>(t.ToArray()); // copy of t
```
- ForEach

```list1.ForEach(i => list2.Add(i));```
- ConvertAll()

```
namespace Delegates
{
    class X
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }
 
    class Y
    {
        public int Id { get; set; }
        public string Name { get; set; }
    }
 
    class Program
    {
        static void Main(string[] args)
        {
            List<X> x = new List<X>();
            for (int i = 0; i < 100; i++)
                x.Add(new X { Id = i, Name = string.Format("x_{0}", i.ToString()) });
            // copy x to y
            List<Y> y = new List<Y>(x.ConvertAll<Y>(e => { return new Y { Id = e.Id, Name = e.Name }; }));
            Debug.Assert(x.Count == y.Count);
        }
 
    }
}
```