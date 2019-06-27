## Data Persistence


#data seeding
https://docs.microsoft.com/en-us/ef/core/modeling/data-seeding

3 way to do it


TodoItemDataContext.cs
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
with the method above you have to know in advance the ids of the entities (even if they are identity), and in large hierarchical structures is a problem. Futhermore you couldn't have declared the foreing keys that entityframework added for you by convetions to the db, so you won't be able to add these "ids" at all.
A more versatile approach is to create the migration as usual  `dotnet ef migrations add migrationname` 
then apply the migration either manually `dotnet ef database update` or automatically:

in Startup.cs
```C#
var serviceScopeFactory = app.ApplicationServices.GetService<IServiceScopeFactory>();
using (var scope = serviceScopeFactory.CreateScope())
{
    var context = (TodoContext)scope.ServiceProvider.GetService(typeof(TodoContext));
    context.Database.Migrate(); //it applies existing migrations - the same result of "dotnet ef database update"
}
```

At last seeding data...



????

https://stackoverflow.com/questions/42355481/auto-create-database-in-entity-framework-core/42356110

context.Database.EnsureCreated()