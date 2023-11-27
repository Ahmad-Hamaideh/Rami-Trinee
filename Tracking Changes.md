
# ✨ Tracking Changes of Entities





```bash

                        يتم تتبع التغييرات تلقائيًا عندما تقوم بالتفاعل مع الكائنات (Entities) في سياق
```


###  1. إحضار الكائنات من قاعدة البيانات



```c#
using (var context = new YourDbContext())
{
    // استرجاع الكائن من قاعدة البيانات
    var entity = context.YourEntities.Find(1);
}

```



###  2. تغيير الكائن:


```c#
entity.Property1 = "قيمة جديدة";

```


###  3. الحفاظ على التغييرات:


```c#
context.SaveChanges();


```
### 4. فحص التغييرات بشكل صريح:



```c#
var changes = context.ChangeTracker.Entries()
    .Where(e => e.State == EntityState.Modified)
    .ToList();


```
### 5. تعطيل تتبع التغييرات:




```c#
var entities = context.YourEntities.AsNoTracking().ToList();


```
