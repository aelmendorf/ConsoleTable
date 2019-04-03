# ConsoleTable

Simple Console table generator.

```
ConsoleTable partTable = new ConsoleTable();
PropertyInfo[] partProperties = typeof(Part).GetProperties();
partTable.Columns = (from property in partProperties
                     where property.PropertyType != typeof(ICollection<Lot>) && property.PropertyType != typeof(ICollection<Product_Category_Field>)
                     select property.Name).ToList<object>();
context.Parts.ToList().ForEach(part => {
    List<object> row = new List<object>();
    foreach (PropertyInfo info in partProperties)
    {
        if (info.PropertyType != typeof(ICollection<Lot>) && info.PropertyType != typeof(ICollection<Product_Category_Field>))
        {
            row.Add(info.GetValue(part));
        }
    }
    partTable.AddRow(row.ToArray());
});
Console.WriteLine(partTable.ToString());
Console.WriteLine("Press Any Key to Exit");
Console.ReadKey();

```

