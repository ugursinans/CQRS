# CQRS + Mediator Pattern
.NET core 7 ile CQRS + Mediator Pattern  RabbitMq (Redis + SqlServer) ile Uygulandığı bir örnek. 

WriteApi ve ReadApi içerisinde api versionlama kullanıldı. Swagger ile de arayüzde deprecated olmayan version default gözükmek üzere çalışıyor.
Swagger özelinde XML dosyası kullanılarak Swagger arayüzü güzelleştirildi. Hatta swagger için css de kullandım.(wwwroot>swagger-ui)
WriteApi SQL server kullanıyor. Verileri kaydederken aynı zamanda rabbitMQ daki ilgili kuyruğa event bilgisi ile birlikte entity gönderiyor.
ReadApi Redis ten verileri okuyor.
Consumer_WS bir worker service olarak geliştirildi. RabbitMq da kuyruğa eklenen verileri consume edip, redis e basıyor. Burada eventual consistency mevcut. CQRS in tek gördüğüm drawback i bu gibi.

DDD yaklaşımını uygulamaya çalıştım. Features klasörü içeriğinden bunu anlayabilirsiniz. Query ve Command isimlendirmeleri bir domainin bir businessina işaret ediyor. EventType gibi bir alan da DB de saklanıyor.

Çok falza geliştirme yapmadım sonuçta bir proje yapmıyordum. Desenleri tam olarak uygulayabildiğim redis ve rabbitmq yu da kullandığım güzel birörnek oldu bence.

bu servisler dockerize edilebilir ben henüz etmedim.
kubernates de pub lar ile de yönetilebilir. Bir sonraki çalışmam bunun üzerine olacak.

EF Core code first kullandım. Burada entity framework default olara nvarchar kullanıyordu bunları varchar a çektim gerekli uzunlukları verdim.

deprecate olmuş WriteApi sürümü görseli:docv1
![image](https://github.com/ugursinans/CQRS/assets/17143493/5dd4ae1e-d14e-4ae0-afc0-5e7ef78923b2)
deprecate olmayan WriteApi sürümü görseli: docv2
![image](https://github.com/ugursinans/CQRS/assets/17143493/be4679d4-ec02-4dea-9d2e-33f2725cfa2d)

redis görseli:
![image](https://github.com/ugursinans/CQRS/assets/17143493/406ff254-2e3c-4927-8294-42830cc01cdc)


docker görseli:
![image](https://github.com/ugursinans/CQRS/assets/17143493/57ec251c-bd9f-41e8-846b-a672658d6503)


rabbitmq görseli: tek kuyruk var, durable= true, autoack= false
![image](https://github.com/ugursinans/CQRS/assets/17143493/bcc487b4-27a6-4838-be90-7b32c899eeb6)
