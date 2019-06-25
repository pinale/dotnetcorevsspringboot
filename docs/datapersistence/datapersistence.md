## Data Persistence


#data seeding
https://docs.microsoft.com/en-us/ef/core/modeling/data-seeding

3 way to do it

```C#
modelBuilder.Entity<Blog>().HasData(new Blog {BlogId = 1, Url = "http://sample.com"});
```
