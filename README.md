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

