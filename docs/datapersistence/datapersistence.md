## Data Persistence


#data seeding
https://docs.microsoft.com/en-us/ef/core/modeling/data-seeding

3 way to do it

```C#
protected override void OnModelCreating(ModelBuilder modelBuilder){

    var seed = new TodoItem[]  {
        new TodoItem() { Id= 1, IsComplete=true, Name = "Alessio"},
        new TodoItem() { Id= 2, IsComplete=true, Name = "Ida"},
        new TodoItem() { Id= 3, IsComplete=true, Name = "Samuel"},
        new TodoItem() { Id= 4, IsComplete=true, Name = "Emily"}
    };
    modelBuilder.Entity<TodoItem>().HasData(seed);
}

```

and than create and apply the migration...
```
dotnet ef migrations add seeddata
dotnet ef database update
```
