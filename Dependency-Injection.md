
# ✨  Dependency Injection





```bash



             هو أن تسمح ل كود أخر بأن يقوم بالأستدعاء بدلا من أن تقوم به

```


###  Creat interface  & class


```c#
// IMyNameService.cs
public interface IMyNameService
{
    string GetName();
}

// MyNameService.cs
public class MyNameService : IMyNameService
{
    public string GetName()
    {
        return "John Doe";
    }
}
```



###  Add Services

```c#
// program.cs

    services.AddTransient<IMyNameService, MyNameService>();

```
 (Service Lifetimes):
 
Transient: يتم إعادة إنشاء الخدمة في كل مرة يتم فيها طلبها.

Scoped: يتم إنشاء الخدمة مرة واحدة لكل طلب HTTP. في نطاق الطلب الواحد، تكون نفس الخدمة متاحة لجميع الطلبات.

Singleton: يتم إنشاء الخدمة مرة واحدة فقط وتظل قائمة طوال فترة حياة التطبيق.



```c#
// MyController.cs
public class MyController : Controller
{
    private readonly IMyNameService _myNameService;

    public MyController(IMyNameService myNameService)
    {
        _myNameService = myNameService;
    }

    public IActionResult Index()
    {
        var name = _myNameService.GetName();
        ViewData["Name"] = name; // تخزين الاسم في ViewData ليتم استخدامه في العرض

        return View();
    }
}

```
```bash
Dependency Injection
نلاحظ الفائدة  حيث أن التغيير تم في مكان واحد فقط.

```
