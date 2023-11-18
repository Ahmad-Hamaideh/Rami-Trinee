
# Data Access & EF Core 👽

Ado.net ==> مجموعة من الكلاسات الي بتخليني اقدر اتواصل مع  مصادر البيانات 


## Connection string 🧵

---> appsting.josn
```c#

  "constr" :  "Server = . ; Database = DigitalCurrency ; Integrated Security = SSPI ; TrustServerCertificate = True"

```
---> program.cs
```c#

var configuration = new ConfigurationBuilder()
                .AddJsonFile("appsettings.json")
                .Build();


IDbConnection db = new SqlConnection(configuration.GetSection("constr").Value);
```

##Dapper ❤️‍🔥

🔸Dapper عبارة عن Micro-ORM وتختص بعملية الوصول لقاعدة البيانات
🔸وهي طبقة تكون فوق ado.net 



```c#
//المثال هو نقل مبلغ 2000 من سارة😶‍🌫️ الى مينى 

    // Transfer 2000
            // From: id 8   Sarah   10000
            // To: id 4   Menna   5500

            decimal amountToTranfer = 2000m;

            using (var transactionScope = new TransactionScope())
            {
                // sarah
                var walletFrom = db.QuerySingle<Wallet>
                  ("SELECT * FROM Wallets Where Id = @Id", new {Id = 8});
            
                // Menna
                var walletTo = db.QuerySingle<Wallet>
                  ("SELECT * FROM Wallets Where Id = @Id", new { Id = 4 }); 

                db.Execute("UPDATE Wallets Set Balance = @Balance Where Id = @Id",
                    new
                    {
                        Id = walletFrom.Id,
                        Balance = walletFrom.Balance - amountToTranfer
                    }
                ); ;

                db.Execute("UPDATE Wallets Set Balance = @Balance Where Id = @Id",
                  new
                  {
                      Id = walletTo.Id,
                      Balance = walletTo.Balance + amountToTranfer
                  }
                );
                transactionScope.Complete();

            }

            Console.ReadKey();
        }
```



