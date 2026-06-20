# PHP Repo

Katalog referensi ekosistem PHP modern: framework, library, tooling, CMS, testing, security, deployment, dan package yang masih cocok dipakai untuk project baru.

> Terakhir ditinjau: 20 Juni 2026.  
> Fokus utama: PHP modern, Composer, package aktif, dan pilihan yang aman untuk project produksi.

## Ringkasan rekomendasi cepat

| Kebutuhan | Pilihan utama | Alternatif kuat | Catatan |
|---|---|---|---|
| Full-stack web app | Laravel 13 | Symfony 7.4 LTS / 8.x | Laravel paling cepat untuk produk; Symfony kuat untuk enterprise dan komponen reusable. |
| API backend | Laravel, Symfony, API Platform | Slim, Mezzio | Pilih berdasarkan ukuran tim dan kompleksitas domain. |
| Microservice ringan | Slim 4 | Mezzio, Spiral | Cocok untuk API kecil, webhook, gateway, dan service internal. |
| CMS | WordPress, Drupal, Joomla | Grav, October CMS, Statamic | WordPress tetap populer; Drupal/Joomla lebih cocok untuk struktur konten besar. |
| E-commerce | WooCommerce, Magento / Adobe Commerce | Sylius, PrestaShop, Shopware | WooCommerce cepat untuk UMKM; Magento/Sylius lebih kuat untuk enterprise. |
| Testing | PHPUnit, Pest | Codeception, Behat | PHPUnit standar; Pest lebih ringkas dan modern. |
| Static analysis | PHPStan, Psalm | Phan | Wajib untuk codebase serius. |
| Code style | Laravel Pint, PHP-CS-Fixer, PHP_CodeSniffer | Easy Coding Standard | Gunakan CI agar standar konsisten. |
| HTTP client | Guzzle 7 | Symfony HttpClient | Guzzle sangat umum; Symfony HttpClient ringan dan modern. |
| Database / ORM | Eloquent, Doctrine ORM | Cycle ORM, Atlas ORM | Eloquent cocok Laravel; Doctrine cocok enterprise/domain complex. |
| Queue / async | Laravel Queue, Symfony Messenger | RoadRunner, Swoole, ReactPHP, AMPHP | Pilih sesuai kebutuhan real-time dan worker. |
| AI / ML | Laravel AI SDK, PHP-ML | OpenAI PHP client, LLPhant | Area berkembang; cek versi terbaru sebelum produksi. |

## Versi PHP yang disarankan

| Target | Rekomendasi | Alasan |
|---|---|---|
| Project baru | PHP 8.4 atau 8.5 | Aman untuk jangka menengah dan kompatibel dengan framework modern. |
| Laravel terbaru | PHP 8.3+ | Laravel 13 membutuhkan minimal PHP 8.3. |
| Symfony modern | PHP 8.2+ sampai 8.4+ | Symfony 7.4 LTS butuh PHP 8.2+; Symfony 8.x butuh PHP 8.4+. |
| Hindari | PHP 7.x, 8.0, 8.1 untuk project baru | Cabang lama sudah atau segera keluar dari dukungan utama. |

## Core ecosystem

| Package / Project | Versi line yang cocok | Install | Kegunaan | Status |
|---|---:|---|---|---|
| PHP | 8.4 / 8.5 | Sesuai OS / Docker | Runtime utama | Recommended |
| Composer | 2.x | `composer self-update` | Dependency manager PHP | Wajib |
| Packagist | - | - | Registry package Composer | Wajib |
| PHP-FIG PSR | PSR-4, PSR-7, PSR-11, PSR-12, PSR-15, PSR-18 | - | Standar interoperabilitas | Wajib dipahami |
| Docker PHP images | 8.4 / 8.5 | `php:8.4-fpm`, `php:8.5-cli` | Runtime konsisten | Recommended |

## Framework web dan API

| Project | Composer | Versi line | Cocok untuk | Catatan |
|---|---|---:|---|---|
| Laravel | `composer create-project laravel/laravel app` | 13.x | Full-stack app, SaaS, API, admin panel, queue | Pilihan paling produktif untuk mayoritas project baru. |
| Symfony | `composer create-project symfony/skeleton app` | 7.4 LTS / 8.x | Enterprise, reusable components, API besar | 7.4 untuk LTS; 8.x untuk fitur terbaru. |
| CodeIgniter 4 | `composer create-project codeigniter4/appstarter app` | 4.x | App ringan, migrasi dari CI lama | Gunakan CodeIgniter 4, bukan repo `bcit-ci/CodeIgniter` lama. |
| CakePHP | `composer create-project cakephp/app app` | 5.x | CRUD cepat, convention-over-configuration | Kuat untuk aplikasi bisnis tradisional. |
| Yii | `composer create-project yiisoft/app app` | 3.x | App modern berbasis package Yii baru | Yii 2 masih dipakai, tapi project baru sebaiknya cek kesiapan Yii 3. |
| Slim | `composer require slim/slim slim/psr7` | 4.x | Micro API, webhook, middleware app | Minimalis dan cepat. |
| Mezzio | `composer create-project mezzio/mezzio-skeleton app` | 3.x | PSR middleware, enterprise API | Bagian dari ekosistem Laminas. |
| Laminas MVC | `composer create-project laminas/laminas-mvc-skeleton app` | 3.x | Enterprise legacy-modern PHP | Penerus Zend Framework. |
| Spiral | `composer create-project spiral/app app` | 3.x | Long-running app, RoadRunner, microservice | Cocok untuk performa tinggi. |
| Hyperf | `composer create-project hyperf/hyperf-skeleton app` | 3.x | Coroutine, Swoole, microservice | Cocok untuk backend high concurrency. |
| Phalcon | Extension + framework package | 5.x | Performa tinggi berbasis extension | Perlu instalasi extension C. |

## CMS, blog, dan e-commerce

| Project | Versi line | Kegunaan | Status |
|---|---:|---|---|
| WordPress | 6.x | CMS/blog paling populer | Recommended untuk konten umum. |
| WooCommerce | 9.x / 10.x | E-commerce WordPress | Cocok untuk UMKM sampai menengah. |
| Drupal | 11.x | CMS enterprise / structured content | Cocok untuk portal kompleks. |
| Joomla | 5.x / 6.x | CMS general purpose | Masih relevan untuk situs konten. |
| Grav | 1.7+ | Flat-file CMS | Ringan, tanpa database. |
| October CMS | 3.x / 4.x | CMS Laravel-based | Cocok untuk developer Laravel. |
| Statamic | 5.x | Flat-file / Laravel CMS | Bagus untuk konten modern dan developer experience. |
| Magento / Adobe Commerce | 2.4.x | E-commerce enterprise | Berat, tetapi kuat untuk katalog besar. |
| Sylius | 2.x | Headless / composable commerce | Cocok untuk custom commerce. |
| PrestaShop | 8.x / 9.x | E-commerce open source | Alternatif toko online mandiri. |
| Shopware | 6.x | Commerce modern | Banyak dipakai di ekosistem Symfony. |
| OpenCart | 4.x | E-commerce sederhana | Cocok untuk toko kecil-menengah. |
| Matomo | 5.x | Web analytics self-hosted | Pengganti modern nama lama Piwik. |
| Nextcloud | 31+ / 32+ | Cloud file collaboration | Cocok untuk self-hosted storage. |
| phpMyAdmin | 5.x | Web UI MySQL/MariaDB | Admin database klasik. |
| Adminer | 4.x / 5.x | Single-file DB admin | Ringan dan praktis. |

## HTTP, API, dan integrasi

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| Guzzle | `composer require guzzlehttp/guzzle` | 7.x | HTTP client populer. |
| Symfony HttpClient | `composer require symfony/http-client` | 7.4 / 8.x | HTTP client modern dan efisien. |
| PSR-7 Nyholm | `composer require nyholm/psr7` | 1.x | Implementasi PSR-7 ringan. |
| PHP-HTTP Discovery | `composer require php-http/discovery` | 1.x | Discovery client PSR. |
| API Platform | `composer require api` pada Symfony / distribusi API Platform | 4.x | REST/GraphQL API otomatis. |
| Laravel Sanctum | `composer require laravel/sanctum` | 4.x | Token auth ringan untuk Laravel. |
| Laravel Passport | `composer require laravel/passport` | 13.x | OAuth2 server untuk Laravel. |
| league/oauth2-server | `composer require league/oauth2-server` | 9.x | OAuth2 server framework-agnostic. |
| firebase/php-jwt | `composer require firebase/php-jwt` | 6.x | JWT sederhana. |
| lcobucci/jwt | `composer require lcobucci/jwt` | 5.x | JWT lebih strict dan typed. |
| google/apiclient | `composer require google/apiclient` | 2.x | Google API client. |
| aws/aws-sdk-php | `composer require aws/aws-sdk-php` | 3.x | AWS SDK untuk PHP. |

## Database, ORM, migration, cache, dan search

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| Doctrine ORM | `composer require doctrine/orm` | 3.x | ORM enterprise. |
| Doctrine DBAL | `composer require doctrine/dbal` | 4.x | Database abstraction layer. |
| Eloquent | `composer require illuminate/database` | 13.x | ORM Laravel standalone. |
| Cycle ORM | `composer require cycle/orm` | 2.x | ORM modern berbasis schema. |
| CakePHP Phinx | `composer require robmorgan/phinx` | 0.16+ | Database migration. |
| Predis | `composer require predis/predis` | 3.x | Redis client PHP. |
| ext-redis | PECL | 6.x | Redis extension performa tinggi. |
| Monolog | `composer require monolog/monolog` | 3.x | Logging standar. |
| Meilisearch PHP | `composer require meilisearch/meilisearch-php` | 1.x | Search engine modern. |
| Elasticsearch PHP | `composer require elasticsearch/elasticsearch` | 8.x | Elasticsearch client. |
| ramsey/uuid | `composer require ramsey/uuid` | 4.x | UUID. |
| symfony/uid | `composer require symfony/uid` | 7.4 / 8.x | UUID/ULID modern. |

## Template, frontend bridge, dan asset

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| Twig | `composer require twig/twig` | 3.x | Template engine modern. |
| Blade standalone | `composer require illuminate/view` | 13.x | Blade tanpa full Laravel. |
| Livewire | `composer require livewire/livewire` | 3.x | UI interaktif Laravel tanpa SPA penuh. |
| Inertia.js Laravel adapter | `composer require inertiajs/inertia-laravel` | 2.x | Bridge Laravel + Vue/React/Svelte. |
| Symfony UX | `composer require symfony/ux-turbo` | 2.x | Interaksi modern di Symfony. |
| Vite Laravel Plugin | `composer require laravel/vite-plugin` | 1.x / 2.x | Asset bundling modern Laravel. |

## Form, validation, date, string, dan helper

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| Carbon | `composer require nesbot/carbon` | 3.x | Date/time API. |
| Respect Validation | `composer require respect/validation` | 2.x | Validation fluent. |
| Symfony Validator | `composer require symfony/validator` | 7.4 / 8.x | Validator enterprise. |
| Symfony String | `composer require symfony/string` | 7.4 / 8.x | Unicode string helper. |
| Symfony Translation | `composer require symfony/translation` | 7.4 / 8.x | I18n/translation. |
| Symfony Console | `composer require symfony/console` | 7.4 / 8.x | CLI command. |
| Laravel Collections | `composer require illuminate/collections` | 13.x | Collection helper. |
| league/commonmark | `composer require league/commonmark` | 2.x | Markdown parser modern. |
| Parsedown | `composer require erusev/parsedown` | 1.x | Markdown parser ringan; cek keamanan dan kebutuhan. |

## File, storage, image, PDF, spreadsheet, dan dokumen

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| Flysystem | `composer require league/flysystem` | 3.x | Abstraction filesystem. |
| Intervention Image | `composer require intervention/image` | 3.x | Manipulasi gambar. |
| Imagine | `composer require imagine/imagine` | 1.x | Image manipulation alternatif. |
| Dompdf | `composer require dompdf/dompdf` | 3.x | HTML ke PDF. |
| mPDF | `composer require mpdf/mpdf` | 8.x | PDF dari HTML dengan fitur kuat. |
| TCPDF | `composer require tecnickcom/tcpdf` | 6.x | PDF klasik. |
| PhpSpreadsheet | `composer require phpoffice/phpspreadsheet` | 2.x / 3.x / 4.x | Spreadsheet modern; pengganti PHPExcel. |
| PHPWord | `composer require phpoffice/phpword` | 1.x | Dokumen Word. |
| Laravel Excel | `composer require maatwebsite/excel` | 3.x | Import/export Excel untuk Laravel. |
| Spatie Media Library | `composer require spatie/laravel-medialibrary` | 11.x | Media management Laravel. |

## Mail, notification, dan realtime

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| Symfony Mailer | `composer require symfony/mailer` | 7.4 / 8.x | Mailer modern. |
| PHPMailer | `composer require phpmailer/phpmailer` | 6.x | Email klasik dan stabil. |
| Laravel Notifications | Built-in Laravel | 13.x | Notification channel. |
| Pusher PHP Server | `composer require pusher/pusher-php-server` | 7.x | WebSocket broadcast. |
| Ratchet | `composer require cboden/ratchet` | 0.4+ | WebSocket server PHP klasik. |
| ReactPHP | `composer require react/event-loop` | 1.x | Event loop async. |
| AMPHP | `composer require amphp/amp` | 3.x | Async PHP modern. |
| OpenSwoole / Swoole | PECL / Composer bridge | 22.x / 5.x+ | High-performance async server. |
| Workerman | `composer require workerman/workerman` | 5.x | Async server sederhana. |
| RoadRunner | Binary + Composer packages | 2025.x | PHP application server. |
| Laravel Octane | `composer require laravel/octane` | 2.x | Laravel high-performance server. |

## Testing, quality assurance, static analysis, dan refactor

| Tool | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| PHPUnit | `composer require --dev phpunit/phpunit` | 12.x / 13.x | Unit testing standar PHP. |
| Pest | `composer require --dev pestphp/pest` | 3.x / 4.x | Testing modern dan ringkas. |
| Codeception | `composer require --dev codeception/codeception` | 5.x | Acceptance/functional testing. |
| Behat | `composer require --dev behat/behat` | 3.x | BDD testing. |
| Mockery | `composer require --dev mockery/mockery` | 1.x | Mock object. |
| PHPStan | `composer require --dev phpstan/phpstan` | 2.x | Static analysis. |
| Psalm | `composer require --dev vimeo/psalm` | 6.x | Static analysis alternatif. |
| Phan | `composer require --dev phan/phan` | 5.x | Static analyzer. |
| Rector | `composer require --dev rector/rector` | 2.x | Automated refactor/upgrade. |
| PHP-CS-Fixer | `composer require --dev friendsofphp/php-cs-fixer` | 3.x | Code style fixer. |
| PHP_CodeSniffer | `composer require --dev squizlabs/php_codesniffer` | 3.x / 4.x | Code style checker. |
| Laravel Pint | `composer require --dev laravel/pint` | 1.x | Formatter Laravel. |
| Infection | `composer require --dev infection/infection` | 0.29+ | Mutation testing. |
| Deptrac | `composer require --dev qossmic/deptrac` | 2.x | Dependency architecture checker. |
| Composer Normalize | `composer require --dev ergebnis/composer-normalize` | 2.x | Rapikan composer.json. |

## Security dan dependency audit

| Tool / Package | Composer | Kegunaan | Status |
|---|---|---|---|
| Composer audit | `composer audit` | Cek advisory dependency | Wajib di CI. |
| Roave Security Advisories | `composer require --dev roave/security-advisories:dev-latest` | Mencegah instalasi package rentan | Recommended. |
| Symfony Security Bundle | `composer require symfony/security-bundle` | Security stack Symfony | Recommended untuk Symfony. |
| Laravel Sanctum | `composer require laravel/sanctum` | API token auth | Recommended untuk Laravel API ringan. |
| ParagonIE Sodium Compat | `composer require paragonie/sodium_compat` | Crypto compatibility | Gunakan jika environment butuh fallback. |
| Defuse PHP Encryption | `composer require defuse/php-encryption` | Enkripsi aplikasi | Cocok untuk use case tertentu. |
| spatie/laravel-permission | `composer require spatie/laravel-permission` | Role & permission Laravel | Populer dan matang. |
| scheb/2fa-bundle | `composer require scheb/2fa-bundle` | 2FA Symfony | Cocok untuk Symfony. |

## Data, fake data, scraping, crawler, dan parser

| Package | Composer | Versi line | Kegunaan |
|---|---|---:|---|
| FakerPHP | `composer require --dev fakerphp/faker` | 1.x | Fake data; pengganti `fzaninotto/faker`. |
| Symfony DomCrawler | `composer require symfony/dom-crawler` | 7.4 / 8.x | HTML/XML crawler. |
| Symfony BrowserKit | `composer require symfony/browser-kit` | 7.4 / 8.x | Simulasi browser. |
| Symfony Panther | `composer require --dev symfony/panther` | 2.x | Browser testing/scraping berbasis Chrome. |
| PHP-Parser | `composer require nikic/php-parser` | 5.x | Parser AST PHP. |
| league/csv | `composer require league/csv` | 9.x | CSV reader/writer. |
| GeoCoder PHP | `composer require geocoder-php/google-maps-provider` | 4.x | Geocoding. |
| Mobile Detect | `composer require mobiledetect/mobiledetectlib` | 4.x | Deteksi device; pakai hati-hati, responsive CSS tetap utama. |

## AI, machine learning, dan agentic tooling

| Package / Project | Composer | Kegunaan | Catatan |
|---|---|---|---|
| Laravel AI SDK | Laravel 13 ecosystem | AI primitives, agents, embeddings, vector search | Cocok untuk project Laravel modern. |
| OpenAI PHP Client | `composer require openai-php/client` | Integrasi OpenAI API | Pastikan key aman di `.env`. |
| LLPhant | `composer require theodo-group/llphant` | LLM app framework PHP | Cocok untuk RAG/agent sederhana. |
| PHP-ML | `composer require php-ai/php-ml` | Machine learning klasik di PHP | Cocok untuk pembelajaran/eksperimen. |
| Rubix ML | `composer require rubix/ml` | ML toolkit PHP | Alternatif lebih lengkap untuk ML klasik. |

## DevOps, deployment, observability

| Tool | Install | Kegunaan |
|---|---|---|
| Deployer | `composer require deployer/deployer --dev` | Deployment PHP. |
| Laravel Envoyer / Forge | SaaS | Deploy dan server management Laravel. |
| Symfony CLI | Binary | Local dev, server, cloud integration Symfony. |
| Docker Compose | Binary | Local stack database/cache/app. |
| FrankenPHP | Binary / Docker | Modern PHP app server berbasis Caddy. |
| RoadRunner | Binary | High-performance PHP worker server. |
| Sentry PHP | `composer require sentry/sentry` | Error monitoring. |
| OpenTelemetry PHP | `composer require open-telemetry/api` | Observability/tracing. |
| Monolog | `composer require monolog/monolog` | Logging. |

## Package lama yang sebaiknya diganti

| Lama | Status | Pengganti modern |
|---|---|---|
| `fzaninotto/Faker` | Tidak lagi jadi pilihan utama | `fakerphp/faker` |
| `PHPOffice/PHPExcel` | Deprecated / digantikan | `phpoffice/phpspreadsheet` |
| `swiftmailer/swiftmailer` | Deprecated | `symfony/mailer` atau `phpmailer/phpmailer` |
| `silexphp/Silex` | End-of-life | Symfony, Slim, Laravel, Mezzio |
| `bcit-ci/CodeIgniter` | CodeIgniter 3 legacy | `codeigniter4/CodeIgniter4` |
| `piwik/piwik` | Nama lama | Matomo |
| `phacility/phabricator` | Tidak cocok untuk project baru | GitHub / GitLab / Gitea / Forgejo |
| `facebookarchive/facebook-php-sdk` | Archived | SDK resmi terbaru atau OAuth client modern |
| `mgp25/Chat-API` | Risiko tinggi / tidak resmi | WhatsApp Business Cloud API resmi |
| `kriswallsmith/assetic` | Legacy asset pipeline | Vite, Symfony AssetMapper, Laravel Vite |
| `FriendsOfPHP/Goutte` | Legacy scraping stack | Symfony BrowserKit, DomCrawler, Panther |
| `tymondesigns/jwt-auth` | Masih ada, tapi pilih hati-hati | Laravel Sanctum, Passport, lcobucci/jwt |

## Template composer.json untuk project PHP modern

### Library umum

```json
{
  "require": {
    "php": "^8.4 || ^8.5",
    "guzzlehttp/guzzle": "^7.0",
    "monolog/monolog": "^3.0",
    "vlucas/phpdotenv": "^5.0",
    "nesbot/carbon": "^3.0"
  },
  "require-dev": {
    "phpunit/phpunit": "^12.0 || ^13.0",
    "phpstan/phpstan": "^2.0",
    "friendsofphp/php-cs-fixer": "^3.0",
    "rector/rector": "^2.0"
  },
  "autoload": {
    "psr-4": {
      "App\\": "src/"
    }
  },
  "scripts": {
    "test": "phpunit",
    "analyse": "phpstan analyse src --level=8",
    "style": "php-cs-fixer fix --dry-run --diff",
    "audit": "composer audit"
  }
}
```

### Laravel modern

```bash
composer create-project laravel/laravel app
cd app
composer require laravel/sanctum spatie/laravel-permission
composer require --dev pestphp/pest phpstan/phpstan laravel/pint rector/rector
php artisan install:api
```

### Symfony modern

```bash
composer create-project symfony/skeleton app
cd app
composer require webapp security orm maker validator serializer twig
composer require --dev phpunit/phpunit phpstan/phpstan friendsofphp/php-cs-fixer rector/rector
```

### Micro API ringan

```bash
mkdir app && cd app
composer require slim/slim slim/psr7 guzzlehttp/guzzle monolog/monolog vlucas/phpdotenv
composer require --dev phpunit/phpunit phpstan/phpstan friendsofphp/php-cs-fixer
```

## Checklist memilih package PHP

1. Cek update terakhir di Packagist dan GitHub.
2. Pilih package yang mendukung PHP 8.4/8.5 untuk project baru.
3. Hindari package archived, abandoned, atau tidak jelas maintainer-nya.
4. Jalankan `composer audit` sebelum deploy.
5. Gunakan semantic version constraint seperti `^13.0`, `^7.4`, atau `^3.0`.
6. Tambahkan testing, static analysis, dan formatter sejak awal.
7. Jangan simpan secret di repository; gunakan `.env` dan secret manager.
8. Untuk project jangka panjang, prioritaskan LTS atau package dengan jadwal support jelas.

## Prioritas belajar / build

1. PHP 8.4/8.5 fundamentals, Composer, PSR-4 autoloading.
2. Laravel 13 untuk full-stack dan API cepat.
3. Symfony Components untuk arsitektur enterprise.
4. PHPUnit/Pest, PHPStan, Rector, PHP-CS-Fixer.
5. Security: composer audit, auth, validation, encryption, rate limiting.
6. Deployment: Docker, Nginx/Caddy, PHP-FPM/FrankenPHP, queue worker, scheduler.
7. Observability: log, tracing, error monitoring.
8. AI integration: Laravel AI SDK, OpenAI PHP client, vector search, queue-based processing.

## Catatan kontribusi

Repository ini bukan daftar mutlak semua package PHP. Tujuannya adalah menjadi peta awal yang rapi, aman, dan mudah dipakai untuk memilih teknologi PHP yang masih relevan.

Saat menambahkan item baru, gunakan format:

```md
| Nama | Composer command | Versi line | Kegunaan | Status |
```

Status yang disarankan:

- `Recommended` untuk project baru.
- `Stable` untuk package matang dan masih aktif.
- `Legacy` untuk package lama yang masih sering ditemui.
- `Avoid for new projects` untuk package yang sebaiknya tidak dipakai di project baru.
