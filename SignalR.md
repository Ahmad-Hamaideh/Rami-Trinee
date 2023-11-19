
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
```Html

<div class="text-center" style="padding : 80px">
   <div class="row">
       <div class="col-md-6" style="    background-color: #c3ffeba3;
    padding: 50px;
    border: 104px">
           <span> enter youe name : </span> <bR />
           <input  type="text" id="txtUser" />  <bR /><bR />
           <span> enter youe massage : </span> <bR />
            <textarea rows="8" cols="30" id="message"> </textarea> <br />  <bR />
           <button type="submit" id="btn" class="btn btn-info"> Send Massege </button>
       </div>
       <BR />
       <div class="col-md-6">
           <h3>Massege List</h3>
            <ul id="list" class="alert alert-info" style="    color: #055160;
                                                     background-color: #cff4fc;
                                                     border-color: #b6effb;
                                                                padding: 57px;">

           </ul>
       </div>
   </div>
</div>

<a href="~/lib/jquery/dist/jquery.min.map"></a>


<script src="~/js/clintt.js"></script>

<script src="~/lib/signalr/dist/browser/signalr.min.js"></script>


```

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
