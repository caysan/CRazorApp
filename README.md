Bu projeyi bir süre sonra yayınlayacağım. Kullanılıyor ancak halen bitmemiş bölümleri var. Authentication/Authorization bölümleri yapım aşamasında halen. 

## Amaç
Proje, genel olarak, ortak bir ortamda birden fazla modül üzerinde kurumsal uygulama geliştiren ekipler için oluşturuldu. 
Servis mimarisi altyapısında, ancak arayüzü tek olacak şekilde, ekiplerin birbirinin kodlarına ve çalışmasına doğrudan müdahale edebilmesinin önüne geçilmesi amaçlanmıştır. Yazılım ekibinin .NET ekibi olduğu ve arayüz ekranlarının da yine bu ekip tarafından, angular-react-vue gibi js frameworklerine girmeden, single page olarak çalışabilmesi için Blazor kullanılmıştır.

![Topoloji](https://raw.githubusercontent.com/caysan/CRazorApp/main/IMG-20230921-WA0000.jpg "Topoloji")

Projea alt yapısı, aşağıdaki isterleri karşılamak amacıyla oluşturulmuştur.
- **Veritabanı tek ve ilişkili olacak**
	- *Veritabanı projede MsSqlserver olarak tek veritabanı kullanıldı. Log lar için ayrı DB bağlantısı yapılabilmekte.*
	- *Her modül, ortak veritabanından, kendisinin kullanacağı tabloların modellerini,"Model Wrapper"oluşturarak modüle entegre eder. *
- Birden fazla modül olsun. Her modülün yazılım ekibi ayrı olsun, çalışırken ekipler birbirinin kodlarına dokunmasın
	- Modüller birbirinden bağımsız çalışır. Her modül ekibi bir Solution altında çalışır, diğerlerinin koduna ulaşmaz. 
- Uygulama servis tabanlı olsun
	- .net Web Api altyapısı kullanılmıştır.
- Arayüz single page olsun ama ekibimiz .net ekibi. Arayüzü bu arkadaşlar da kolaylıkla yapabilsin, react angular gibi uğraştırmasın.
	- Arayüz, single page olması amacıyla Blazor kullanılmıştır. Yazılım ekibinin .net ekibi olduğu varsayılarak geliştirildi. Böylelikle, yazılım geliştirme ekibi arayüzü yine .net c# kullanarak geliştirecektir.
- Arayüz tek olsun, tek bir sayfadan çalışsın. Ekiplerin hazırladığı arayüz yapıları, tek arayüz altında toplansın. Sitedeki kullanıcı yetkisine göre arayüzler değişsin.
	- Modül arayüzleri, yayınlanırken ortak kullanılan APPUI altında birleştirilir. Kullanıcı yetkisine göre bu arayüzler gösterilir. 
- Proje halka açık değil, kurum içi yazılım olacak.
	- Geliştirilen proje, altyapısında blazor web assembly kullanır. Bu sebeple web sitesi tarzında yoğun ziyaretçi kullanımına uygun olmayabilir. blazor webassembly, kullanıcı tarayıcılarına kütüphaneleri ile birlikte yüklenir ve bir web sitesinden daha yüklüdür. 
- Yetkilendirme esnek olsun. Kayıt bazlı yetkilendirme olsun
	- Authentication, .net Entity ve JWT ile gerçekleştirilmektedir. 
	- Authorization yapısı, .net identity ve claim bazlı kullanılır. Multi-tenant yetkilendirme mantığını kullanır. Farklı olarak, Table-Key-Value şeklinde roller/gruplar oluşturularak, kayıt bazlı yetki verilebilme imkanı sağlayacaktır. Her request de, tabloya göre bu istekler sorguda araya eklenir. (Halen yapım aşamasında)

## Kullanılan Teknolojiler
- .Net 7.0
- .Net Blazor Web Assembly
- MS SqlServer
- Redis
- RabbitMQ
- JWT, 

### Kullanılan 3.Parti Kütüphane ve Araçlar
- Telerik Blazor  (Blazor için şimdilik gördüğüm en problemsiz UI arayüzü)
- Telerik DataSource  (Paging işlemleri için hızlı ve efektif kullanımı var)
- FluentValidation
- Redis
- NLog
- Mapster		(automapper dan daha kolay olduğu için...)
- Refit	(UI üzerinden servisteki metodlara doğrudan ulaşabilmek için...)
- EF Core Power Tools
- Unit Of Work Design Pattern
