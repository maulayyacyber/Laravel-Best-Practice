## Laravel Best Practice

**Environment variable**

Gunakan file `.env` untuk menyimpan beberapa informasi penting dan memanggilnya melalui fungsi `env`. Kita tidak dibenarkan membuat atau meletakkan informasi penting di dalam controller dan model apalagi sampai push ke Git.

Contoh Baik :

```
// .env 

API_HOST=https://example.com/api
API_USERNAME=myuser
API_PASSWORD=secret

// memanggil value dari file app/config.php

return [
    ...
    'api_host' => env('API_HOST', 'https://defaultdomain.com')
    'api_username' => env('API_USER', 'defaultuser')
    'api_password' => env('API_USER', 'defaultpassword')
    ...
]
```

Contoh Buruk :

```
define('API_HOST', 'https://defaultdomain.com');
define('API_USERNAME', 'defaultuser');
define('API_PASSWORD', 'defaultpassword');

class DomainController extends Controller
{
    public function index()
    {
      $api_username   
    }
}
```



**Package Configuration**

Disarankan menggunakan `snake_case` untuk penamaan file configuration, kurang lebih contohnya seperti berikut ini :

Contoh Baik :

```
config/my_config.php
```

Contoh Buruk :

```
config/MyConfig.php
```

Kemudian gunakan juga index file config menggunakan `snake_case`, kurang lebih seperti berikut ini :

Contoh Baik :

```
return [
    'my_api' => [
        'domain' => env('API_DOMAIN'),
        'secret' => env('API_SECRET'),
    ]
]
```

Contoh Buruk :

```
return [
    'MyApi' => [
        'DOMAIN' => env('API_DOMAIN'),
        'SECRET' => env('API_SECRET'),
    ]
]
```

**Fat models, skinny controllers**

Letakkan semua logika terkait DB ke dalam model Eloquent atau ke dalam kelas Repositori jika Anda menggunakan Query Builder atau query Sql.

Contoh Buruk :

```
public function index()
{
    $clients = Client::verified()
        ->with(['orders' => function ($q) {
            $q->where('created_at', '>', Carbon::today()->subWeek());
        }])
        ->get();

    return view('index', ['clients' => $clients]);
}
```

Contoh Baik :

```
// app/Http/Controllers/ClientController.php

public function index()
{
    return view('index', ['clients' => $this->client->getWithNewOrders()]);
}


// app/Models/Client.php

class Client extends Model
{
    public function getWithNewOrders()
    {
        return $this->verified()
            ->with(['orders' => function ($q) {
                $q->where('created_at', '>', Carbon::today()->subWeek());
            }])
            ->get();
    }
}
```

**Naming Conventions**

Pada bagian ini kita akan belajar tentang Naming Conventions atau penamaan yang benar sesuai dengan mengikuti umumnya dari para komunitas Laravel di seluruh Dunia.

**Controllers**

Nama controller umumnya dimulai dengan kata benda dalam bentuk tunggal (singular) kemudian diikuti dengan kata, kurang lebih contonya seperti berikut ini :

Contoh Baik :

```
class ArticleController extends Controller
{
    ...
}
```

Contoh Buruk :

```
class ArticlesController extends Controller
{
    ...
}
class wp_articlesController extends Controller
{
    ...
}
class Article extends Controller
{
    ...
}
```

Gunakan penamaan nama method/function dari Resources Controller kurang lebih seperti berikut ini :

Contoh Baik :

```
class ArticleController extends Controller
{
    public function index()
    {
        // list articles
    }
 
    public function create()
    {
        // show create form
    } 

    public function store(Request $request)
    {
        // handle the form POST
    } 

    public function show($id)
    {
        // show a single article
    } 

    public function edit($id)
    {
        // show edit page
    } 

    public function update(Request $request, $id)
    {
        // handle show edit page POST
    } 

    public function destroy($id)
    {
        // delete a article
    } 
}
```

**Naming Conventions**

Pada bagian ini kita akan belajar tentang Naming Conventions atau penamaan yang benar sesuai dengan mengikuti umumnya dari para komunitas Laravel di seluruh Dunia.

**Controllers**

Nama controller umumnya dimulai dengan kata benda dalam bentuk tunggal (singular) kemudian diikuti dengan kata, kurang lebih contonya seperti berikut ini :

Contoh Baik :

```
class ArticleController extends Controller
{
    ...
}
```

Contoh Buruk :

```
class ArticlesController extends Controller
{
    ...
}
class wp_articlesController extends Controller
{
    ...
}
class Article extends Controller
{
    ...
}
```

------

Gunakan penamaan nama method/function dari Resources Controller kurang lebih seperti berikut ini :

Contoh Baik :

```
class ArticleController extends Controller
{
    public function index()
    {
        // list articles
    }
 
    public function create()
    {
        // show create form
    } 

    public function store(Request $request)
    {
        // handle the form POST
    } 

    public function show($id)
    {
        // show a single article
    } 

    public function edit($id)
    {
        // show edit page
    } 

    public function update(Request $request, $id)
    {
        // handle show edit page POST
    } 

    public function destroy($id)
    {
        // delete a article
    } 
}
```

Contoh Buruk :

```
class ArticleController extends Controller
{
    public function list()
    {
        // list articles
    } 

    public function create_or_save()
    {
        // show create form then handle save
    } 

    public function show_edit($id)
    {
        // show a single article then show edit page
    } 

    public function delete($id)
    {
        // delete a article
    } 
}
```

------

