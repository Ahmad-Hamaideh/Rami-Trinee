
# SignalR 🎃

حيث يمكن للمستخدمين ادخال اسم، والدخول إلى صفحة المحادثة وارسال الرسائل بوقت حقيقي بدون تأخير.

المكتبة الرئيسية المستخدمة

`Microsoft.AspNet.SignalR`   



# ✨ Steps


### 🔸 Download  SignalR LIB 



```c#
Add Clint Side lib 
@aspnet/SignalR/
```

### 🔸 Creat Viwe 


### 🔸Creat Folder (HUBS) 
on folder add class (useres) 

```c#
using Microsoft.AspNetCore.SignalR;

namespace SignalR.hops
{
    public class useres : Hub
    {
        public async Task sendMessage(string user, string message)
        {
            await Clients.All.SendAsync("ReceiveMessage", user, message);
        }
    }
}

```

### 🔸 Program.cs

==> add Services
```c#
builder.Services.AddSignalR();

```
```c#
app.UseEndpoints(endpoints =>
{
    endpoints.MapHub<HUP>("/chatHub");  //(must same name in js )
    endpoints.MapControllerRoute(
        name: "default",
        pattern: "{controller=Home}/{action=Index}/{id?}");
});
```
### 🔸 js file

==> add connection 
```c#

var connection = new signalR.HubConnectionBuilder().withUrl("/chatHub").build();


```
```c#
connection.on("ReceiveMessage", function (fromUser, message) {
    var msg = fromUser + " : " + message;
    var li = document.createElement("li");
    li.textContent = msg;
    $("#list").prepend(li);
});

connection.start();

$("#btn").on("click", function () {
    var fromUser = $("#txtUser").val();
    var message = $("#message").val();
    connection.invoke("sendMessage", fromUser, message);
});

```
