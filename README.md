# PHP Repo

A modern PHP ecosystem catalog covering frameworks, libraries, tooling, CMS platforms, testing, security, deployment, observability, AI/ML, and legacy packages that should be reviewed before use.

> Last reviewed: June 20, 2026  
> Main target: PHP 8.4/8.5, Composer 2.x, actively maintained packages, safe dependency choices, and practical options for new projects.  
> Note: patch versions change quickly. For the latest patch number, run `composer outdated`, `composer show vendor/package --all`, and check the official release page.

## Status legend

| Status | Meaning |
|---|---|
| Recommended | Safe and practical for new projects. |
| Stable | Still useful, but choose based on your actual project needs. |
| Advanced | Best for specialized performance or architecture requirements. |
| Specialized | Good for a specific use case, but not always necessary. |
| Legacy/Review | Useful for old projects or learning, but do not automatically start new projects with it. |
| Avoid for new projects | Avoid for new projects; use a modern replacement instead. |

## Quick recommendations

| Need | Primary choice | Alternative | Notes |
| --- | --- | --- | --- |
| New PHP runtime | PHP 8.5 | PHP 8.4 / PHP 8.3 | Use PHP 8.5 for new projects when dependencies are ready; PHP 8.4 remains a safe modern target. |
| Full-stack web app | Laravel 13 | Symfony 7.4 LTS / Symfony 8.x | Laravel is the fastest route for product delivery; Symfony is excellent for enterprise architecture. |
| API backend | Laravel 13 + Sanctum/Passport | Symfony + API Platform, Slim 4, Mezzio | Choose based on domain complexity, team skill, and deployment model. |
| Microservice | Slim 4 | Mezzio, Spiral, Hyperf | Best for webhooks, internal APIs, gateways, and small services. |
| CMS | WordPress | Drupal, Joomla, Grav, Statamic, October CMS | WordPress is the broadest option; Drupal/Joomla fit structured content and larger portals. |
| E-commerce | WooCommerce | Magento/Adobe Commerce, Sylius, PrestaShop, Shopware | WooCommerce is fast for small businesses; Sylius/Magento/Shopware are stronger for complex commerce. |
| Testing | PHPUnit | Pest, Codeception, Behat | PHPUnit remains the standard; Pest is more expressive and concise. |
| Static analysis | PHPStan | Psalm, Phan | Mandatory for serious long-term PHP codebases. |
| Code style | Laravel Pint | PHP-CS-Fixer, PHP_CodeSniffer, Easy Coding Standard | Run code style checks in CI. |
| Security audit | composer audit | Roave Security Advisories | Minimum baseline before deployment. |
| Async / realtime | Laravel Octane | RoadRunner, Swoole/OpenSwoole, ReactPHP, AMPHP, Workerman | Use only when long-running workers, high concurrency, or realtime flows are required. |
| AI / LLM | Laravel AI SDK | OpenAI PHP client, LLPhant, PHP-ML, Rubix ML | Fast-moving category; pin versions and check changelogs before production. |

## Popular versions vs latest suitable versions

| Technology | Modern/latest line | Suggested constraint | Popular/stable line | Notes |
| --- | --- | --- | --- | --- |
| PHP | 8.5 | 8.5.x | 8.4.x / 8.3.x | Recommended runtime target for new projects. |
| Composer | 2.x | 2.9.x+ | 2.8.x | Required dependency manager for modern PHP. |
| Laravel | 13.x | ^13.0 | ^12.0 | Laravel 13 requires PHP 8.3+. |
| Symfony | 8.x / 7.4 LTS | ^8.0 or ^7.4 | 7.4 LTS | Use 7.4 for LTS stability; use 8.x for newest features. |
| WordPress | 7.x / 6.x | Latest stable | 6.x | Use the latest secure release available from WordPress.org. |
| Drupal | 11.x | ^11 | ^10 | Strong option for enterprise content modeling. |
| Joomla | 6.x / 5.x | Latest stable | 5.x | Joomla 6 is the modern line; 5.x remains relevant during migration. |
| PHPUnit | 12.x / 13.x | ^12.0 or ^13.0 | ^11.5 | Choose based on PHP and framework compatibility. |
| Pest | 4.x | ^4.0 | ^3.0 | Modern expressive testing layer. |
| PHPStan | 2.x | ^2.0 | ^1.12 | Primary static analysis choice. |
| Rector | 2.x | ^2.0 | ^1.0 | Automated upgrades and refactors. |
| Guzzle | 7.x | ^7.0 | 7.x | Most common PHP HTTP client. |
| Monolog | 3.x | ^3.0 | ^2.0 | Standard logging library. |
| Twig | 3.x | ^3.0 | 3.x | Modern template engine. |

## Recommended stack presets

### 1. Modern Laravel full-stack / API

```bash
composer create-project laravel/laravel app
cd app
composer require laravel/sanctum spatie/laravel-permission
composer require --dev pestphp/pest phpstan/phpstan laravel/pint rector/rector
php artisan install:api
composer audit
```

Best for SaaS, dashboards, REST APIs, queue workers, AI integrations, and fast business product development.

### 2. Symfony enterprise / large API

```bash
composer create-project symfony/skeleton app
cd app
composer require webapp security orm maker validator serializer twig
composer require --dev phpunit/phpunit phpstan/phpstan friendsofphp/php-cs-fixer rector/rector
composer audit
```

Best for complex domains, modular architecture, enterprise systems, event-driven applications, and API Platform.

### 3. Lightweight micro API

```bash
mkdir app && cd app
composer init
composer require slim/slim slim/psr7 guzzlehttp/guzzle monolog/monolog vlucas/phpdotenv
composer require --dev phpunit/phpunit phpstan/phpstan friendsofphp/php-cs-fixer
composer audit
```

Best for webhooks, small services, internal gateways, lightweight HTTP workers, and fast prototypes.

### 4. Reusable PHP library

```bash
composer init
mkdir -p src tests
composer require psr/log
composer require --dev phpunit/phpunit phpstan/phpstan friendsofphp/php-cs-fixer rector/rector
composer dump-autoload
```

Use PSR-4, semantic versioning, tests, static analysis, and CI from the beginning.

## Web and API frameworks

| Name | Package/Repo | Version line | Install | Status | Best for |
| --- | --- | --- | --- | --- | --- |
| Laravel | laravel/laravel | 13.x | `composer create-project laravel/laravel app` | Recommended | Full-stack apps, SaaS, dashboards, APIs, queues, AI-ready products. |
| Symfony | symfony/skeleton / symfony/symfony | 8.x / 7.4 LTS | `composer create-project symfony/skeleton app` | Recommended | Enterprise systems, modular apps, APIs, reusable components. |
| CodeIgniter 4 | codeigniter4/appstarter | 4.x | `composer create-project codeigniter4/appstarter app` | Stable | Small apps and teams migrating from older CodeIgniter versions. |
| CakePHP | cakephp/app | 5.x | `composer create-project cakephp/app app` | Stable | Business CRUD apps with strong conventions. |
| Slim | slim/slim | 4.x | `composer require slim/slim slim/psr7` | Recommended | Micro APIs, webhooks, middleware-based apps. |
| Mezzio | mezzio/mezzio-skeleton | 3.x | `composer create-project mezzio/mezzio-skeleton app` | Stable | PSR middleware applications and enterprise APIs. |
| Laminas MVC | laminas/laminas-mvc-skeleton | 3.x | `composer create-project laminas/laminas-mvc-skeleton app` | Stable | Modernized Zend-style enterprise applications. |
| Spiral | spiral/app | 3.x | `composer create-project spiral/app app` | Advanced | RoadRunner, long-running workers, high-performance services. |
| Hyperf | hyperf/hyperf-skeleton | 3.x | `composer create-project hyperf/hyperf-skeleton app` | Advanced | Coroutine/Swoole-based high-concurrency services. |
| Phalcon | phalcon/cphalcon | 5.x | Extension + Composer packages | Specialized | High-performance applications that can support a C extension dependency. |
| Yii | yiisoft/yii2 / Yii packages | 2.x stable / 3.x ecosystem | `composer create-project yiisoft/yii2-app-basic app` | Review | Yii 2 is mature; review Yii 3 ecosystem readiness before starting new work. |
| Fat-Free Framework | bcosca/fatfree | 3.x | `composer require bcosca/fatfree-core` | Lightweight | Small and simple PHP applications. |
| Flight | flightphp/core | 3.x | `composer require flightphp/core` | Lightweight | Small APIs and micro apps. |
| Nette | nette/application | 3.x | `composer require nette/application` | Stable | Mature framework ecosystem, especially popular in Europe. |

## CMS, blog, wiki, analytics, and e-commerce

| Name | Repo/Package | Version line | Use case | Status |
| --- | --- | --- | --- | --- |
| WordPress | wordpress/wordpress-develop | Latest stable | General CMS, blogs, marketing sites | Recommended |
| WooCommerce | woocommerce/woocommerce | 10.x | WordPress e-commerce | Recommended for small and mid-sized stores |
| Drupal | drupal/core-recommended | 11.x | Enterprise CMS and structured content | Recommended for complex content |
| Joomla | joomla/joomla-cms | 6.x / 5.x | General-purpose CMS | Stable |
| Grav | getgrav/grav | 1.7+ | Flat-file CMS | Recommended for lightweight sites |
| October CMS | octobercms/october | 3.x / 4.x | Laravel-based CMS | Stable |
| Statamic | statamic/cms | 5.x | Laravel CMS with flat-file/database options | Recommended |
| Craft CMS | craftcms/cms | 5.x | Content-first developer-friendly CMS | Strong option |
| TYPO3 | typo3/cms | 13 LTS | Enterprise CMS | Strong option |
| Magento / Adobe Commerce | magento/magento2 | 2.4.x | Enterprise e-commerce | Heavy but powerful |
| Sylius | sylius/sylius | 2.x | Composable/headless commerce | Recommended for custom commerce |
| PrestaShop | prestashop/prestashop | 9.x / 8.x | Open-source e-commerce | Stable |
| Shopware | shopware/shopware | 6.x | Modern commerce platform | Strong Symfony ecosystem |
| OpenCart | opencart/opencart | 4.x | Simple online stores | Stable |
| Matomo | matomo-org/matomo | 5.x | Self-hosted analytics | Recommended |
| Nextcloud | nextcloud/server | 31+ / 32+ | Self-hosted cloud collaboration | Recommended |
| BookStack | BookStackApp/BookStack | 25.x+ | Documentation/wiki platform | Recommended |
| DokuWiki | splitbrain/dokuwiki | Stable | Database-free wiki | Stable |
| MediaWiki | wikimedia/mediawiki | 1.43+ / 1.44+ | Large wiki systems | Stable |
| Mautic | mautic/mautic | 5.x / 6.x | Marketing automation | Specialized |

## HTTP, API, authentication, integrations, and payments

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| Guzzle | guzzlehttp/guzzle | 7.x | `composer require guzzlehttp/guzzle` | Popular HTTP client. |
| Symfony HttpClient | symfony/http-client | 7.4 / 8.x | `composer require symfony/http-client` | Modern efficient HTTP client. |
| Nyholm PSR-7 | nyholm/psr7 | 1.x | `composer require nyholm/psr7` | Lightweight PSR-7 implementation. |
| API Platform | api-platform/core | 4.x | `composer require api` | REST/GraphQL API platform for Symfony and Laravel. |
| webonyx/graphql-php | webonyx/graphql-php | 15.x | `composer require webonyx/graphql-php` | GraphQL server library. |
| swagger-php | zircote/swagger-php | 5.x | `composer require zircote/swagger-php` | OpenAPI generator using annotations/attributes. |
| NelmioApiDocBundle | nelmio/api-doc-bundle | 5.x | `composer require nelmio/api-doc-bundle` | Symfony API documentation. |
| Laravel Sanctum | laravel/sanctum | 4.x | `composer require laravel/sanctum` | Lightweight token authentication for Laravel. |
| Laravel Passport | laravel/passport | 13.x | `composer require laravel/passport` | OAuth2 server for Laravel. |
| league/oauth2-server | league/oauth2-server | 9.x | `composer require league/oauth2-server` | Framework-agnostic OAuth2 server. |
| lcobucci/jwt | lcobucci/jwt | 5.x | `composer require lcobucci/jwt` | Strict typed JWT library. |
| firebase/php-jwt | firebase/php-jwt | 6.x | `composer require firebase/php-jwt` | Simple JWT library. |
| stripe-php | stripe/stripe-php | 16.x+ | `composer require stripe/stripe-php` | Stripe payments. |
| twilio-php | twilio/sdk | 8.x | `composer require twilio/sdk` | SMS, voice, and WhatsApp integrations through Twilio. |
| AWS SDK PHP | aws/aws-sdk-php | 3.x | `composer require aws/aws-sdk-php` | AWS integrations. |
| Google API Client | google/apiclient | 2.x | `composer require google/apiclient` | Google API integrations. |
| GitHub API PHP | knplabs/github-api | 3.x | `composer require knplabs/github-api` | GitHub REST API client. |

## Database, ORM, cache, search, and data models

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| Eloquent ORM | illuminate/database | 13.x | `composer require illuminate/database` | Standalone Laravel ORM. |
| Doctrine ORM | doctrine/orm | 3.x | `composer require doctrine/orm` | Enterprise ORM for complex domains. |
| Doctrine DBAL | doctrine/dbal | 4.x | `composer require doctrine/dbal` | Database abstraction layer. |
| Cycle ORM | cycle/orm | 2.x | `composer require cycle/orm` | Modern schema-based ORM. |
| Propel | propel/propel | 2.x | `composer require propel/propel` | Alternative ORM. |
| Phinx | robmorgan/phinx | 0.16+ | `composer require robmorgan/phinx` | Database migrations. |
| Predis | predis/predis | 3.x | `composer require predis/predis` | Redis client written in PHP. |
| ext-redis | phpredis | 6.x | PECL | High-performance Redis extension. |
| Elasticsearch PHP | elasticsearch/elasticsearch | 8.x | `composer require elasticsearch/elasticsearch` | Official Elasticsearch client. |
| Elastica | ruflin/elastica | 8.x | `composer require ruflin/elastica` | Elasticsearch abstraction layer. |
| Meilisearch PHP | meilisearch/meilisearch-php | 1.x | `composer require meilisearch/meilisearch-php` | Modern search engine client. |
| TNTSearch | teamtnt/tntsearch | 2.x | `composer require teamtnt/tntsearch` | Full-text search in PHP. |
| league/csv | league/csv | 9.x | `composer require league/csv` | CSV reader/writer. |
| moneyphp/money | moneyphp/money | 4.x | `composer require moneyphp/money` | Money value objects. |
| ramsey/uuid | ramsey/uuid | 4.x | `composer require ramsey/uuid` | UUID generation. |
| symfony/uid | symfony/uid | 7.4 / 8.x | `composer require symfony/uid` | UUID/ULID utilities. |

## Testing, quality assurance, static analysis, and refactoring

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| PHPUnit | phpunit/phpunit | 12.x / 13.x | `composer require --dev phpunit/phpunit` | Standard unit testing framework. |
| Pest | pestphp/pest | 4.x | `composer require --dev pestphp/pest` | Modern expressive testing layer. |
| Codeception | codeception/codeception | 5.x | `composer require --dev codeception/codeception` | Acceptance and functional testing. |
| Behat | behat/behat | 3.x | `composer require --dev behat/behat` | BDD testing. |
| Mockery | mockery/mockery | 1.x | `composer require --dev mockery/mockery` | Mock objects. |
| PHPStan | phpstan/phpstan | 2.x | `composer require --dev phpstan/phpstan` | Primary static analysis tool. |
| Psalm | vimeo/psalm | 6.x | `composer require --dev vimeo/psalm` | Alternative static analysis tool. |
| Phan | phan/phan | 5.x | `composer require --dev phan/phan` | Static analyzer. |
| Rector | rector/rector | 2.x | `composer require --dev rector/rector` | Automated refactoring and upgrades. |
| PHP-CS-Fixer | friendsofphp/php-cs-fixer | 3.x | `composer require --dev friendsofphp/php-cs-fixer` | Code style fixer. |
| PHP_CodeSniffer | squizlabs/php_codesniffer | 3.x / 4.x | `composer require --dev squizlabs/php_codesniffer` | Code style checker. |
| Laravel Pint | laravel/pint | 1.x | `composer require --dev laravel/pint` | Laravel-focused formatter. |
| Infection | infection/infection | 0.29+ | `composer require --dev infection/infection` | Mutation testing. |
| Deptrac | qossmic/deptrac | 2.x | `composer require --dev qossmic/deptrac` | Architecture dependency checker. |
| GrumPHP | phpro/grumphp | 2.x | `composer require --dev phpro/grumphp` | Pre-commit quality gate. |
| PhpMetrics | phpmetrics/phpmetrics | 3.x | `composer require --dev phpmetrics/phpmetrics` | Code metrics. |

## Files, storage, images, PDF, spreadsheets, and media

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| Flysystem | league/flysystem | 3.x | `composer require league/flysystem` | Filesystem abstraction. |
| Intervention Image | intervention/image | 3.x | `composer require intervention/image` | Image manipulation. |
| Imagine | imagine/imagine | 1.x | `composer require imagine/imagine` | Alternative image manipulation library. |
| Dompdf | dompdf/dompdf | 3.x | `composer require dompdf/dompdf` | HTML to PDF conversion. |
| mPDF | mpdf/mpdf | 8.x | `composer require mpdf/mpdf` | UTF-8 HTML to PDF generation. |
| TCPDF | tecnickcom/tcpdf | 6.x | `composer require tecnickcom/tcpdf` | Classic PDF and barcode generation. |
| Browsershot | spatie/browsershot | 4.x | `composer require spatie/browsershot` | Screenshot/PDF generation through a browser engine. |
| PhpSpreadsheet | phpoffice/phpspreadsheet | 2.x / 3.x / 4.x | `composer require phpoffice/phpspreadsheet` | Modern spreadsheet library; replacement for PHPExcel. |
| PHPWord | phpoffice/phpword | 1.x | `composer require phpoffice/phpword` | Word document generation and reading. |
| Laravel Excel | maatwebsite/excel | 3.x | `composer require maatwebsite/excel` | Excel import/export for Laravel. |
| Spatie Media Library | spatie/laravel-medialibrary | 11.x | `composer require spatie/laravel-medialibrary` | Media management for Laravel. |
| PHP-FFMpeg | php-ffmpeg/php-ffmpeg | 1.x | `composer require php-ffmpeg/php-ffmpeg` | Video/audio processing wrapper. |
| Endroid QR Code | endroid/qr-code | 5.x | `composer require endroid/qr-code` | QR code generation. |

## Mail, notifications, queues, async, and realtime

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| Symfony Mailer | symfony/mailer | 7.4 / 8.x | `composer require symfony/mailer` | Modern mailer. |
| PHPMailer | phpmailer/phpmailer | 6.x | `composer require phpmailer/phpmailer` | Classic stable email library. |
| Laravel Notifications | laravel/framework | 13.x | Built-in | Multi-channel notifications. |
| Pusher PHP Server | pusher/pusher-php-server | 7.x | `composer require pusher/pusher-php-server` | Realtime broadcasting. |
| Ratchet | cboden/ratchet | 0.4.x | `composer require cboden/ratchet` | Classic WebSocket server. |
| ReactPHP | react/event-loop | 1.x | `composer require react/event-loop` | Event loop for async PHP. |
| AMPHP | amphp/amp | 3.x | `composer require amphp/amp` | Modern async PHP framework. |
| OpenSwoole/Swoole | openswoole/core / ext-swoole | 22.x / 5.x+ | PECL + Composer | High-concurrency server runtime. |
| Workerman | workerman/workerman | 5.x | `composer require workerman/workerman` | Simple async server. |
| RoadRunner | spiral/roadrunner | 2025.x | Binary + Composer | PHP application server. |
| Laravel Octane | laravel/octane | 2.x | `composer require laravel/octane` | High-performance Laravel server. |
| php-amqplib | php-amqplib/php-amqplib | 3.x | `composer require php-amqplib/php-amqplib` | RabbitMQ/AMQP client. |
| Pheanstalk | pda/pheanstalk | 7.x / 8.x | `composer require pda/pheanstalk` | Beanstalkd queue client. |

## Security and dependency auditing

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| composer audit | Composer built-in | 2.x | `composer audit` | Dependency vulnerability audit. |
| Roave Security Advisories | roave/security-advisories | dev-latest | `composer require --dev roave/security-advisories:dev-latest` | Blocks vulnerable packages during install/update. |
| Symfony Security Bundle | symfony/security-bundle | 7.4 / 8.x | `composer require symfony/security-bundle` | Symfony security stack. |
| spatie/laravel-permission | spatie/laravel-permission | 6.x | `composer require spatie/laravel-permission` | Roles and permissions for Laravel. |
| Bouncer | silber/bouncer | 1.x | `composer require silber/bouncer` | Roles and abilities for Eloquent. |
| Defuse Encryption | defuse/php-encryption | 2.x | `composer require defuse/php-encryption` | Application-level encryption. |
| phpseclib | phpseclib/phpseclib | 3.x | `composer require phpseclib/phpseclib` | Pure PHP SSH/SFTP/crypto utilities. |
| HTML Purifier | ezyang/htmlpurifier | 4.x | `composer require ezyang/htmlpurifier` | HTML sanitization. |
| Google Authenticator | phpgangsta/googleauthenticator | Legacy/review | `composer require phpgangsta/googleauthenticator` | 2FA helper; review modern alternatives before production. |
| iniscan | psecio/iniscan | 0.x/1.x | `composer require --dev psecio/iniscan` | php.ini security scan. |

## Data, fake data, safe scraping, parsers, and utilities

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| FakerPHP | fakerphp/faker | 1.x | `composer require --dev fakerphp/faker` | Fake data; replacement for fzaninotto/faker. |
| Symfony DomCrawler | symfony/dom-crawler | 7.4 / 8.x | `composer require symfony/dom-crawler` | HTML/XML crawler. |
| Symfony BrowserKit | symfony/browser-kit | 7.4 / 8.x | `composer require symfony/browser-kit` | Browser simulation. |
| Symfony Panther | symfony/panther | 2.x | `composer require --dev symfony/panther` | Browser testing/scraping through Chrome. |
| PHP-Parser | nikic/php-parser | 5.x | `composer require nikic/php-parser` | PHP AST parser. |
| league/commonmark | league/commonmark | 2.x | `composer require league/commonmark` | Modern Markdown parser. |
| Parsedown | erusev/parsedown | 1.x | `composer require erusev/parsedown` | Lightweight Markdown parser; review security and maintenance needs. |
| Geocoder PHP | geocoder-php/geocoder | 4.x | `composer require geocoder-php/geocoder` | Geocoding abstraction. |
| Mobile Detect | mobiledetect/mobiledetectlib | 4.x | `composer require mobiledetect/mobiledetectlib` | Device detection; prefer responsive design first. |
| libphonenumber-for-php | giggsey/libphonenumber-for-php | 8.x | `composer require giggsey/libphonenumber-for-php` | Phone number validation. |
| SimplePie | simplepie/simplepie | 1.x | `composer require simplepie/simplepie` | RSS/Atom parsing. |

## AI, machine learning, and agent tooling

| Name | Package | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| Laravel AI SDK | Laravel AI ecosystem | 13.x | Laravel ecosystem | AI primitives, agents, embeddings, audio, image, and vector search patterns. |
| OpenAI PHP Client | openai-php/client | 0.x / 1.x | `composer require openai-php/client` | OpenAI API integration; keep API keys in environment variables. |
| LLPhant | theodo-group/llphant | 0.x/1.x | `composer require theodo-group/llphant` | LLM application and RAG framework for PHP. |
| PHP-ML | php-ai/php-ml | 0.x | `composer require php-ai/php-ml` | Classic machine learning in PHP. |
| Rubix ML | rubix/ml | 2.x | `composer require rubix/ml` | More complete classical ML toolkit. |
| Math PHP | markrogoyski/math-php | 2.x | `composer require markrogoyski/math-php` | Math and statistics utilities. |

## DevOps, deployment, observability, debugging, and profiling

| Name | Package/Tool | Version line | Install | Use case |
| --- | --- | --- | --- | --- |
| Deployer | deployer/deployer | 7.x / 8.x | `composer require --dev deployer/deployer` | PHP deployment automation. |
| Symfony CLI | Binary | Latest | Official installer | Local development and Symfony tooling. |
| Docker Compose | Binary | v2 | Docker Desktop or package manager | Local app/database/cache stack. |
| FrankenPHP | Binary/Docker | 1.x+ | Docker image | Modern PHP application server based on Caddy. |
| RoadRunner | Binary | 2025.x | Binary + config | High-performance PHP workers. |
| Sentry PHP | sentry/sentry | 4.x | `composer require sentry/sentry` | Error monitoring. |
| OpenTelemetry PHP | open-telemetry/api | 1.x | `composer require open-telemetry/api` | Tracing and observability. |
| Monolog | monolog/monolog | 3.x | `composer require monolog/monolog` | Standard logging. |
| PsySH | psy/psysh | 0.12+ | `composer require --dev psy/psysh` | Modern PHP REPL. |
| Kint | kint-php/kint | 6.x | `composer require --dev kint-php/kint` | Debug output. |
| Clockwork | itsgoingd/clockwork | 5.x | `composer require itsgoingd/clockwork` | Development profiling/debugging. |
| DebugBar | maximebf/debugbar | 1.x | `composer require --dev maximebf/debugbar` | Debug toolbar. |

## Legacy packages and modern replacements

| Legacy package | Status | Modern replacement |
| --- | --- | --- |
| fzaninotto/Faker | Abandoned / legacy | fakerphp/faker |
| PHPOffice/PHPExcel | Deprecated | phpoffice/phpspreadsheet |
| swiftmailer/swiftmailer | Deprecated | symfony/mailer or phpmailer/phpmailer |
| silexphp/Silex | End-of-life | Symfony, Slim, Laravel, or Mezzio |
| bcit-ci/CodeIgniter | CodeIgniter 3 legacy | codeigniter4/appstarter |
| piwik/piwik | Old project name | Matomo |
| phacility/phabricator | Not suitable for new projects | GitHub, GitLab, Gitea, or Forgejo |
| facebookarchive/facebook-php-sdk | Archived | Modern OAuth client or official current SDK |
| kriswallsmith/assetic | Legacy asset pipeline | Vite, Symfony AssetMapper, or Laravel Vite |
| FriendsOfPHP/Goutte | Legacy scraping stack | Symfony BrowserKit, DomCrawler, or Panther |
| tymondesigns/jwt-auth | Requires review | Laravel Sanctum, Passport, or lcobucci/jwt |
| amazonwebservices/aws-sdk-for-php | Deprecated v1 | aws/aws-sdk-php v3 |
| PayPal-PHP-SDK | Legacy | Current PayPal checkout/server SDK or modern payment gateway SDK |
| password_compat | Unnecessary for modern PHP | Built-in password_hash/password_verify |
| php7cc | Legacy upgrade tool | Rector + PHPStan |

## Modern `composer.json` template

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
    "fix-style": "php-cs-fixer fix",
    "refactor": "rector process --dry-run",
    "audit": "composer audit"
  }
}
```

## Package selection checklist

1. Check maintenance status on GitHub and Packagist.
2. Prefer packages that support PHP 8.4/8.5 for new projects.
3. Avoid archived, abandoned, or security-unpatched dependencies.
4. Run `composer audit` before deployment.
5. Use clear version constraints such as `^13.0`, `^8.0`, `^7.4`, or `^3.0`.
6. Add tests, static analysis, formatting, and dependency auditing to CI.
7. Never store secrets in the repository; use `.env`, CI secrets, or a secrets manager.
8. For long-term products, prefer LTS lines or projects with clear support policies.
9. For public APIs, include rate limiting, validation, authentication, logging, monitoring, and OpenAPI documentation.
10. For AI/LLM packages, separate the provider layer so models and vendors can be changed later.

## Recommended learning and build order

1. PHP 8.4/8.5, Composer, PSR-4, PSR-12, error handling, typed properties, and attributes.
2. Laravel 13 for full-stack apps, APIs, queues, and productivity.
3. Symfony 7.4 LTS/8.x for enterprise components and modular architecture.
4. PHPUnit/Pest, PHPStan, Rector, PHP-CS-Fixer/Pint.
5. Security: composer audit, authentication, authorization, validation, encryption, and rate limiting.
6. Database work: migrations, ORM, transactions, indexing, caching, and queues.
7. Deployment: Docker, PHP-FPM/FrankenPHP/RoadRunner, schedulers, workers, and logs.
8. Observability: Monolog, Sentry, OpenTelemetry.
9. AI integration: embeddings, vector search, queue-based LLM jobs, and provider abstraction.

## Primary version sources

| Source | URL |
| --- | --- |
| PHP supported versions | https://www.php.net/supported-versions.php |
| Laravel release notes | https://laravel.com/docs/releases |
| Symfony releases | https://symfony.com/releases |
| Composer download | https://getcomposer.org/download/ |
| Packagist | https://packagist.org/ |
| WordPress releases | https://wordpress.org/download/releases/ |
| Drupal core releases | https://www.drupal.org/project/drupal/releases |
| Joomla downloads | https://downloads.joomla.org/latest |

## Appendix A — Legacy reference backlog from the original README

This appendix preserves references from the original list so they are not lost. Not every item below is recommended for new projects. Use the curated categories above first, then review each legacy item before adopting it.

- [laravel/laravel](https://github.com/laravel/laravel)
- [symfony/symfony](https://github.com/symfony/symfony)
- [bcit-ci/CodeIgniter](https://github.com/bcit-ci/CodeIgniter)
- [domnikl/DesignPatternsPHP](https://github.com/domnikl/DesignPatternsPHP)
- [fzaninotto/Faker](https://github.com/fzaninotto/Faker)
- [yiisoft/yii2](https://github.com/yiisoft/yii2)
- [guzzle/guzzle](https://github.com/guzzle/guzzle)
- [composer/composer](https://github.com/composer/composer)
- [PHPMailer/PHPMailer](https://github.com/PHPMailer/PHPMailer)
- [PHPOffice/PHPExcel](https://github.com/PHPOffice/PHPExcel)
- [phacility/phabricator](https://github.com/phacility/phabricator)
- [phalcon/cphalcon](https://github.com/phalcon/cphalcon)
- [piwik/piwik](https://github.com/piwik/piwik)
- [getgrav/grav](https://github.com/getgrav/grav)
- [cakephp/cakephp](https://github.com/cakephp/cakephp)
- [serbanghita/Mobile-Detect](https://github.com/serbanghita/Mobile-Detect)
- [CachetHQ/Cachet](https://github.com/CachetHQ/Cachet)
- [sebastianbergmann/phpunit](https://github.com/sebastianbergmann/phpunit)
- [octobercms/october](https://github.com/octobercms/october)
- [briannesbitt/Carbon](https://github.com/briannesbitt/Carbon)
- [barryvdh/laravel-debugbar](https://github.com/barryvdh/laravel-debugbar)
- [Intervention/image](https://github.com/Intervention/image)
- [FriendsOfPHP/Goutte](https://github.com/FriendsOfPHP/Goutte)
- [owncloud/core](https://github.com/owncloud/core)
- [overtrue/wechat](https://github.com/overtrue/wechat)
- [walkor/Workerman](https://github.com/walkor/Workerman)
- [FriendsOfPHP/PHP-CS-Fixer](https://github.com/FriendsOfPHP/PHP-CS-Fixer)
- [magento/magento2](https://github.com/magento/magento2)
- [deployphp/deployer](https://github.com/deployphp/deployer)
- [yiisoft/yii](https://github.com/yiisoft/yii)
- [tymondesigns/jwt-auth](https://github.com/tymondesigns/jwt-auth)
- [erusev/parsedown](https://github.com/erusev/parsedown)
- [google/google-api-php-client](https://github.com/google/google-api-php-client)
- [pagekit/pagekit](https://github.com/pagekit/pagekit)
- [filp/whoops](https://github.com/filp/whoops)
- [php-ai/php-ml](https://github.com/php-ai/php-ml)
- [Respect/Validation](https://github.com/Respect/Validation)
- [top-think/think](https://github.com/top-think/think)
- [humhub/humhub](https://github.com/humhub/humhub)
- [jupeter/clean-code-php](https://github.com/jupeter/clean-code-php)
- [squizlabs/PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- [dompdf/dompdf](https://github.com/dompdf/dompdf)
- [Maatwebsite/Laravel-Excel](https://github.com/Maatwebsite/Laravel-Excel)
- [vlucas/phpdotenv](https://github.com/vlucas/phpdotenv)
- [twigphp/Twig](https://github.com/twigphp/Twig)
- [woocommerce/woocommerce](https://github.com/woocommerce/woocommerce)
- [ratchetphp/Ratchet](https://github.com/ratchetphp/Ratchet)
- [opencart/opencart](https://github.com/opencart/opencart)
- [nrk/predis](https://github.com/nrk/predis)
- [dodgepudding/wechat-php-sdk](https://github.com/dodgepudding/wechat-php-sdk)
- [typecho/typecho](https://github.com/typecho/typecho)
- [silexphp/Silex](https://github.com/silexphp/Silex)
- [Sylius/Sylius](https://github.com/Sylius/Sylius)
- [thephpleague/flysystem](https://github.com/thephpleague/flysystem)
- [kriswallsmith/assetic](https://github.com/kriswallsmith/assetic)
- [abraham/twitteroauth](https://github.com/abraham/twitteroauth)
- [facebookarchive/facebook-php-sdk](https://github.com/facebookarchive/facebook-php-sdk)
- [mgp25/Chat-API](https://github.com/mgp25/Chat-API)
- [timber/timber](https://github.com/timber/timber)
- [bolt/bolt](https://github.com/bolt/bolt)
- [YOURLS/YOURLS](https://github.com/YOURLS/YOURLS)
- [wp-cli/wp-cli](https://github.com/wp-cli/wp-cli)
- [mledoze/countries](https://github.com/mledoze/countries)
- [php-pm/php-pm](https://github.com/php-pm/php-pm)
- [cakephp/phinx](https://github.com/cakephp/phinx)
- [thephpleague/oauth2-server](https://github.com/thephpleague/oauth2-server)
- [invoiceninja/invoiceninja](https://github.com/invoiceninja/invoiceninja)
- [geocoder-php/Geocoder](https://github.com/geocoder-php/Geocoder)
- [pattern-lab/patternlab-php](https://github.com/pattern-lab/patternlab-php)
- [wallabag/wallabag](https://github.com/wallabag/wallabag)
- [avalanche123/Imagine](https://github.com/avalanche123/Imagine)
- [nikic/PHP-Parser](https://github.com/nikic/PHP-Parser)
- [anchorcms/anchor-cms](https://github.com/anchorcms/anchor-cms)
- [Codeception/Codeception](https://github.com/Codeception/Codeception)
- [chrisboulton/php-resque](https://github.com/chrisboulton/php-resque)
- [kanboard/kanboard](https://github.com/kanboard/kanboard)
- [nextcloud/server](https://github.com/nextcloud/server)
- [botman/botman](https://github.com/botman/botman)
- [catfan/Medoo](https://github.com/catfan/Medoo)
- [rmccue/Requests](https://github.com/rmccue/Requests)
- [PHPOffice/PHPWord](https://github.com/PHPOffice/PHPWord)
- [picocms/Pico](https://github.com/picocms/Pico)
- [PrestaShop/PrestaShop](https://github.com/PrestaShop/PrestaShop)
- [pyrocms/pyrocms](https://github.com/pyrocms/pyrocms)
- [aws/aws-sdk-php](https://github.com/aws/aws-sdk-php)
- [ramsey/uuid](https://github.com/ramsey/uuid)
- [phpmyadmin/phpmyadmin](https://github.com/phpmyadmin/phpmyadmin)
- [hybridauth/hybridauth](https://github.com/hybridauth/hybridauth)
- [bobthecow/mustache.php](https://github.com/bobthecow/mustache.php)
- [top-think/thinkphp](https://github.com/top-think/thinkphp)
- [joomla/joomla-cms](https://github.com/joomla/joomla-cms)
- [michelf/php-markdown](https://github.com/michelf/php-markdown)
- [rocketeers/rocketeer](https://github.com/rocketeers/rocketeer)
- [nikic/FastRoute](https://github.com/nikic/FastRoute)
- [mockery/mockery](https://github.com/mockery/mockery)
- [rappasoft/laravel-5-boilerplate](https://github.com/rappasoft/laravel-5-boilerplate)
- [phan/phan](https://github.com/phan/phan)
- [agentejo/cockpit](https://github.com/agentejo/cockpit)
- [vrana/adminer](https://github.com/vrana/adminer)
- [johnlui/Learn-Laravel-5](https://github.com/johnlui/Learn-Laravel-5)
- [interconnectit/Search-Replace-DB](https://github.com/interconnectit/Search-Replace-DB)
- [KnpLabs/snappy](https://github.com/KnpLabs/snappy)
- [bshaffer/oauth2-server-php](https://github.com/bshaffer/oauth2-server-php)
- [phptodayorg/php-must-watch](https://github.com/phptodayorg/php-must-watch)
- [phpstan/phpstan](https://github.com/phpstan/phpstan)
- [Behat/Behat](https://github.com/Behat/Behat)
- [jokkedk/webgrind](https://github.com/jokkedk/webgrind)
- [BootstrapCMS/CMS](https://github.com/BootstrapCMS/CMS)
- [ivanakimov/hashids.php](https://github.com/ivanakimov/hashids.php)
- [leafo/lessphp](https://github.com/leafo/lessphp)
- [borisrepl/boris](https://github.com/borisrepl/boris)
- [klein/klein.php](https://github.com/klein/klein.php)
- [bobthecow/psysh](https://github.com/bobthecow/psysh)
- [RainLoop/rainloop-webmail](https://github.com/RainLoop/rainloop-webmail)
- [bcosca/fatfree](https://github.com/bcosca/fatfree)
- [php/php-langspec](https://github.com/php/php-langspec)
- [spatie/laravel-permission](https://github.com/spatie/laravel-permission)
- [phalcon/zephir](https://github.com/phalcon/zephir)
- [swiftmailer/swiftmailer](https://github.com/swiftmailer/swiftmailer)
- [phpDocumentor/phpDocumentor2](https://github.com/phpDocumentor/phpDocumentor2)
- [VerbalExpressions/PHPVerbalExpressions](https://github.com/VerbalExpressions/PHPVerbalExpressions)
- [phacility/xhprof](https://github.com/phacility/xhprof)
- [giggsey/libphonenumber-for-php](https://github.com/giggsey/libphonenumber-for-php)
- [danielstjules/Stringy](https://github.com/danielstjules/Stringy)
- [mautic/mautic](https://github.com/mautic/mautic)
- [kint-php/kint](https://github.com/kint-php/kint)
- [panique/huge](https://github.com/panique/huge)
- [phpro/grumphp](https://github.com/phpro/grumphp)
- [spatie/laravel-backup](https://github.com/spatie/laravel-backup)
- [gitscrum-community-edition/laravel-gitscrum](https://github.com/gitscrum-community-edition/laravel-gitscrum)
- [splitbrain/dokuwiki](https://github.com/splitbrain/dokuwiki)
- [facebook/php-webdriver](https://github.com/facebook/php-webdriver)
- [elastic/elasticsearch-php](https://github.com/elastic/elasticsearch-php)
- [ircmaxell/password_compat](https://github.com/ircmaxell/password_compat)
- [facebook/php-graph-sdk](https://github.com/facebook/php-graph-sdk)
- [Atlantic18/DoctrineExtensions](https://github.com/Atlantic18/DoctrineExtensions)
- [KnpLabs/Gaufrette](https://github.com/KnpLabs/Gaufrette)
- [overtrue/pinyin](https://github.com/overtrue/pinyin)
- [summerblue/phphub](https://github.com/summerblue/phphub)
- [consolidation/Robo](https://github.com/consolidation/Robo)
- [php-amqplib/php-amqplib](https://github.com/php-amqplib/php-amqplib)
- [javiereguiluz/EasyAdminBundle](https://github.com/javiereguiluz/EasyAdminBundle)
- [CMB2/CMB2](https://github.com/CMB2/CMB2)
- [joshcam/PHP-MySQLi-Database-Class](https://github.com/joshcam/PHP-MySQLi-Database-Class)
- [mikecao/flight](https://github.com/mikecao/flight)
- [HanSon/vbot](https://github.com/HanSon/vbot)
- [PHP-FFMpeg/PHP-FFMpeg](https://github.com/PHP-FFMpeg/PHP-FFMpeg)
- [SimpleRegex/SRL-PHP](https://github.com/SimpleRegex/SRL-PHP)
- [maximebf/php-debugbar](https://github.com/maximebf/php-debugbar)
- [kalcaddle/KodExplorer](https://github.com/kalcaddle/KodExplorer)
- [jenssegers/agent](https://github.com/jenssegers/agent)
- [yajra/laravel-datatables](https://github.com/yajra/laravel-datatables)
- [gabrielrcouto/php-gui](https://github.com/gabrielrcouto/php-gui)
- [jadjoubran/laravel5-angular-material-starter](https://github.com/jadjoubran/laravel5-angular-material-starter)
- [lcobucci/jwt](https://github.com/lcobucci/jwt)
- [drush-ops/drush](https://github.com/drush-ops/drush)
- [silexphp/Pimple](https://github.com/silexphp/Pimple)
- [erikdubbelboer/phpRedisAdmin](https://github.com/erikdubbelboer/phpRedisAdmin)
- [Xethron/migrations-generator](https://github.com/Xethron/migrations-generator)
- [PHPSocialNetwork/phpfastcache](https://github.com/PHPSocialNetwork/phpfastcache)
- [hmlb/phpunit-vw](https://github.com/hmlb/phpunit-vw)
- [moneyphp/money](https://github.com/moneyphp/money)
- [opauth/opauth](https://github.com/opauth/opauth)
- [spatie/laravel-medialibrary](https://github.com/spatie/laravel-medialibrary)
- [summerblue/phphub5](https://github.com/summerblue/phphub5)
- [tencent-php/tsf](https://github.com/tencent-php/tsf)
- [php-curl-class/php-curl-class](https://github.com/php-curl-class/php-curl-class)
- [ApiGen/ApiGen](https://github.com/ApiGen/ApiGen)
- [cydrobolt/polr](https://github.com/cydrobolt/polr)
- [FriendsOfSymfony/FOSRestBundle](https://github.com/FriendsOfSymfony/FOSRestBundle)
- [matyhtf/framework](https://github.com/matyhtf/framework)
- [corcel/corcel](https://github.com/corcel/corcel)
- [phpseclib/phpseclib](https://github.com/phpseclib/phpseclib)
- [J7mbo/twitter-api-php](https://github.com/J7mbo/twitter-api-php)
- [zircote/swagger-php](https://github.com/zircote/swagger-php)
- [webonyx/graphql-php](https://github.com/webonyx/graphql-php)
- [hwi/HWIOAuthBundle](https://github.com/hwi/HWIOAuthBundle)
- [symfony/symfony-standard](https://github.com/symfony/symfony-standard)
- [ruflin/Elastica](https://github.com/ruflin/Elastica)
- [SSilence/selfoss](https://github.com/SSilence/selfoss)
- [mcamara/laravel-localization](https://github.com/mcamara/laravel-localization)
- [laracasts/PHP-Vars-To-Js-Transformer](https://github.com/laracasts/PHP-Vars-To-Js-Transformer)
- [kakserpom/phpdaemon](https://github.com/kakserpom/phpdaemon)
- [fuel/fuel](https://github.com/fuel/fuel)
- [nelmio/alice](https://github.com/nelmio/alice)
- [JosephLenton/PHP-Error](https://github.com/JosephLenton/PHP-Error)
- [nategood/httpful](https://github.com/nategood/httpful)
- [TGMPA/TGM-Plugin-Activation](https://github.com/TGMPA/TGM-Plugin-Activation)
- [cnvs/canvas](https://github.com/cnvs/canvas)
- [coduo/php-humanizer](https://github.com/coduo/php-humanizer)
- [kriswallsmith/Buzz](https://github.com/kriswallsmith/Buzz)
- [reduxframework/redux-framework](https://github.com/reduxframework/redux-framework)
- [cmgmyr/laravel-messenger](https://github.com/cmgmyr/laravel-messenger)
- [sebastianbergmann/phploc](https://github.com/sebastianbergmann/phploc)
- [sebastianbergmann/phpcpd](https://github.com/sebastianbergmann/phpcpd)
- [defuse/php-encryption](https://github.com/defuse/php-encryption)
- [rap2hpoutre/laravel-log-viewer](https://github.com/rap2hpoutre/laravel-log-viewer)
- [nelmio/NelmioApiDocBundle](https://github.com/nelmio/NelmioApiDocBundle)
- [lincanbin/Carbon-Forum](https://github.com/lincanbin/Carbon-Forum)
- [unicodeveloper/laravel-hackathon-starter](https://github.com/unicodeveloper/laravel-hackathon-starter)
- [phpmetrics/PhpMetrics](https://github.com/phpmetrics/PhpMetrics)
- [walkor/workerman-todpole](https://github.com/walkor/workerman-todpole)
- [immobiliare/ApnsPHP](https://github.com/immobiliare/ApnsPHP)
- [thephpleague/csv](https://github.com/thephpleague/csv)
- [laravel-ardent/ardent](https://github.com/laravel-ardent/ardent)
- [symfony/symfony-docs](https://github.com/symfony/symfony-docs)
- [lixuancn/LaneWeChat](https://github.com/lixuancn/LaneWeChat)
- [phpspec/phpspec](https://github.com/phpspec/phpspec)
- [jpfuentes2/php-activerecord](https://github.com/jpfuentes2/php-activerecord)
- [TIGERB/easy-tips](https://github.com/TIGERB/easy-tips)
- [psecio/iniscan](https://github.com/psecio/iniscan)
- [cosenary/Instagram-PHP-API](https://github.com/cosenary/Instagram-PHP-API)
- [thephpleague/climate](https://github.com/thephpleague/climate)
- [stripe/stripe-php](https://github.com/stripe/stripe-php)
- [paypal/PayPal-PHP-SDK](https://github.com/paypal/PayPal-PHP-SDK)
- [gabrielrcouto/php-terminal-gameboy-emulator](https://github.com/gabrielrcouto/php-terminal-gameboy-emulator)
- [laravelio/portal](https://github.com/laravelio/portal)
- [youzan/zanphp](https://github.com/youzan/zanphp)
- [benkeen/generatedata](https://github.com/benkeen/generatedata)
- [itsgoingd/clockwork](https://github.com/itsgoingd/clockwork)
- [nette/nette](https://github.com/nette/nette)
- [drewm/mailchimp-api](https://github.com/drewm/mailchimp-api)
- [JosephSilber/bouncer](https://github.com/JosephSilber/bouncer)
- [teamtnt/tntsearch](https://github.com/teamtnt/tntsearch)
- [pda/pheanstalk](https://github.com/pda/pheanstalk)
- [overtrue/laravel-wechat](https://github.com/overtrue/laravel-wechat)
- [PHPOffice/PhpSpreadsheet](https://github.com/PHPOffice/PhpSpreadsheet)
- [sstalle/php7cc](https://github.com/sstalle/php7cc)
- [rlerdorf/php7dev](https://github.com/rlerdorf/php7dev)
- [box/spout](https://github.com/box/spout)
- [banago/PHPloy](https://github.com/banago/PHPloy)
- [WhichBrowser/Parser-PHP](https://github.com/WhichBrowser/Parser-PHP)
- [spatie/laravel-analytics](https://github.com/spatie/laravel-analytics)
- [mtdowling/cron-expression](https://github.com/mtdowling/cron-expression)
- [ccampbell/chromephp](https://github.com/ccampbell/chromephp)
- [simplepie/simplepie](https://github.com/simplepie/simplepie)
- [spatie/dashboard.spatie.be](https://github.com/spatie/dashboard.spatie.be)
- [welaika/wordless](https://github.com/welaika/wordless)
- [lazychaser/laravel-nestedset](https://github.com/lazychaser/laravel-nestedset)
- [brianhaveri/Underscore.php](https://github.com/brianhaveri/Underscore.php)
- [KnpLabs/php-github-api](https://github.com/KnpLabs/php-github-api)
- [anandkunal/ToroPHP](https://github.com/anandkunal/ToroPHP)
- [panique/mini](https://github.com/panique/mini)
- [PeeHaa/OpCacheGUI](https://github.com/PeeHaa/OpCacheGUI)
- [cocur/slugify](https://github.com/cocur/slugify)
- [spatie/laravel-activitylog](https://github.com/spatie/laravel-activitylog)
- [eyecatchup/SEOstats](https://github.com/eyecatchup/SEOstats)
- [humbug/humbug](https://github.com/humbug/humbug)
- [gharlan/alfred-github-workflow](https://github.com/gharlan/alfred-github-workflow)
- [backup-manager/backup-manager](https://github.com/backup-manager/backup-manager)
- [nicolaslopezj/searchable](https://github.com/nicolaslopezj/searchable)
- [mevdschee/php-crud-api](https://github.com/mevdschee/php-crud-api)
- [PHP-DI/PHP-DI](https://github.com/PHP-DI/PHP-DI)
- [atoum/atoum](https://github.com/atoum/atoum)
- [mongodb/mongo-php-driver-legacy](https://github.com/mongodb/mongo-php-driver-legacy)
- [php-telegram-bot/core](https://github.com/php-telegram-bot/core)
- [reactjs/react-php-v8js](https://github.com/reactjs/react-php-v8js)
- [UnionOfRAD/lithium](https://github.com/UnionOfRAD/lithium)
- [davejamesmiller/laravel-breadcrumbs](https://github.com/davejamesmiller/laravel-breadcrumbs)
- [Elgg/Elgg](https://github.com/Elgg/Elgg)
- [icicleio/icicle](https://github.com/icicleio/icicle)
- [WordPress-Coding-Standards/WordPress-Coding-Standards](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards)
- [Payum/Payum](https://github.com/Payum/Payum)
- [slimkit/thinksns-plus](https://github.com/slimkit/thinksns-plus)
- [s4n7h0/xvwa](https://github.com/s4n7h0/xvwa)
- [leafo/scssphp](https://github.com/leafo/scssphp)
- [lstrojny/functional-php](https://github.com/lstrojny/functional-php)
- [endroid/QrCode](https://github.com/endroid/QrCode)
- [phpbb/phpbb](https://github.com/phpbb/phpbb)
- [cdevroe/unmark](https://github.com/cdevroe/unmark)
- [goaop/framework](https://github.com/goaop/framework)
- [bcit-ci/CodeIgniter4](https://github.com/bcit-ci/CodeIgniter4)
- [brandonwamboldt/utilphp](https://github.com/brandonwamboldt/utilphp)
- [barbushin/php-console](https://github.com/barbushin/php-console)
- [hightman/scws](https://github.com/hightman/scws)
- [LavaLite/cms](https://github.com/LavaLite/cms)
- [ezyang/htmlpurifier](https://github.com/ezyang/htmlpurifier)
- [thiagoalessio/tesseract-ocr-for-php](https://github.com/thiagoalessio/tesseract-ocr-for-php)
- [FriendsOfPHP/pickle](https://github.com/FriendsOfPHP/pickle)
- [propelorm/Propel2](https://github.com/propelorm/Propel2)
- [neitanod/forceutf8](https://github.com/neitanod/forceutf8)
- [forkcms/forkcms](https://github.com/forkcms/forkcms)
- [Kong/unirest-php](https://github.com/Kong/unirest-php)
- [userfrosting/UserFrosting](https://github.com/userfrosting/UserFrosting)
- [iamcal/php-emoji](https://github.com/iamcal/php-emoji)
- [cartalyst/sentinel](https://github.com/cartalyst/sentinel)
- [Herzult/SimplePHPEasyPlus](https://github.com/Herzult/SimplePHPEasyPlus)
- [justinrainbow/json-schema](https://github.com/justinrainbow/json-schema)
- [wikimedia/mediawiki](https://github.com/wikimedia/mediawiki)
- [tecnickcom/TCPDF](https://github.com/tecnickcom/TCPDF)
- [Lusitanian/PHPoAuthLib](https://github.com/Lusitanian/PHPoAuthLib)
- [PHPGangsta/GoogleAuthenticator](https://github.com/PHPGangsta/GoogleAuthenticator)
- [phpspec/prophecy](https://github.com/phpspec/prophecy)
- [composer/packagist](https://github.com/composer/packagist)
- [phalcon/phalcon-devtools](https://github.com/phalcon/phalcon-devtools)
- [hprose/hprose-php](https://github.com/hprose/hprose-php)
- [madoublet/respond](https://github.com/madoublet/respond)
- [MPOS/php-mpos](https://github.com/MPOS/php-mpos)
- [kraken-php/framework](https://github.com/kraken-php/framework)
- [InvoicePlane/InvoicePlane](https://github.com/InvoicePlane/InvoicePlane)
- [masterexploder/PHPThumb](https://github.com/masterexploder/PHPThumb)
- [amphp/amp](https://github.com/amphp/amp)
- [rinvex/country](https://github.com/rinvex/country)
- [kasperisager/php-dockerized](https://github.com/kasperisager/php-dockerized)
- [PHPixie/Project](https://github.com/PHPixie/Project)
- [jenssegers/imagehash](https://github.com/jenssegers/imagehash)
- [BeatSwitch/lock](https://github.com/BeatSwitch/lock)
- [yohang/Finite](https://github.com/yohang/Finite)
- [helei112g/payment](https://github.com/helei112g/payment)
- [markomarkovic/simple-php-git-deploy](https://github.com/markomarkovic/simple-php-git-deploy)
- [symfony/demo](https://github.com/symfony/demo)
- [Ph3nol/NotificationPusher](https://github.com/Ph3nol/NotificationPusher)
- [maknz/slack](https://github.com/maknz/slack)
- [piwik/device-detector](https://github.com/piwik/device-detector)
- [mpdf/mpdf](https://github.com/mpdf/mpdf)
- [mikehaertl/phpwkhtmltopdf](https://github.com/mikehaertl/phpwkhtmltopdf)
- [reactphp/promise](https://github.com/reactphp/promise)
- [VisualPHPUnit/VisualPHPUnit](https://github.com/VisualPHPUnit/VisualPHPUnit)
- [mvdbos/php-spider](https://github.com/mvdbos/php-spider)
- [phpservermon/phpservermon](https://github.com/phpservermon/phpservermon)
- [irazasyed/telegram-bot-sdk](https://github.com/irazasyed/telegram-bot-sdk)
- [q2a/question2answer](https://github.com/q2a/question2answer)
- [tpyo/amazon-s3-php-class](https://github.com/tpyo/amazon-s3-php-class)
- [causefx/Organizr](https://github.com/causefx/Organizr)
- [apiato/apiato](https://github.com/apiato/apiato)
- [mjaschen/phpgeo](https://github.com/mjaschen/phpgeo)
- [ReactiveX/RxPHP](https://github.com/ReactiveX/RxPHP)
- [nWidart/laravel-modules](https://github.com/nWidart/laravel-modules)
- [aws/aws-sdk-php-laravel](https://github.com/aws/aws-sdk-php-laravel)
- [thephpleague/commonmark](https://github.com/thephpleague/commonmark)
- [BookStackApp/BookStack](https://github.com/BookStackApp/BookStack)
- [paquettg/php-html-parser](https://github.com/paquettg/php-html-parser)
- [hightman/xunsearch](https://github.com/hightman/xunsearch)
- [ErikvdVen/php-gif](https://github.com/ErikvdVen/php-gif)
- [walkor/phpsocket.io](https://github.com/walkor/phpsocket.io)
- [phpsysinfo/phpsysinfo](https://github.com/phpsysinfo/phpsysinfo)
- [meenie/munee](https://github.com/meenie/munee)
- [markrogoyski/math-php](https://github.com/markrogoyski/math-php)
- [hippyvm/hippyvm](https://github.com/hippyvm/hippyvm)
- [Wixel/GUMP](https://github.com/Wixel/GUMP)
- [modxcms/revolution](https://github.com/modxcms/revolution)
- [twilio/twilio-php](https://github.com/twilio/twilio-php)
- [themattharris/tmhOAuth](https://github.com/themattharris/tmhOAuth)
- [miniflux/miniflux](https://github.com/miniflux/miniflux)
- [jonnnnyw/php-phantomjs](https://github.com/jonnnnyw/php-phantomjs)
- [cakephp/debug_kit](https://github.com/cakephp/debug_kit)
- [Tencent/Biny](https://github.com/Tencent/Biny)
- [nette/tracy](https://github.com/nette/tracy)
- [maxmind/GeoIP2-php](https://github.com/maxmind/GeoIP2-php)
- [mewebstudio/captcha](https://github.com/mewebstudio/captcha)
- [craftcms/cms](https://github.com/craftcms/cms)
- [ARCANEDEV/LogViewer](https://github.com/ARCANEDEV/LogViewer)
- [gherkins/regexpbuilderphp](https://github.com/gherkins/regexpbuilderphp)
- [dustin10/VichUploaderBundle](https://github.com/dustin10/VichUploaderBundle)
- [kenjis/php-framework-benchmark](https://github.com/kenjis/php-framework-benchmark)
- [vinkla/laravel-hashids](https://github.com/vinkla/laravel-hashids)
- [thephpleague/geotools](https://github.com/thephpleague/geotools)
- [mantisbt/mantisbt](https://github.com/mantisbt/mantisbt)
- [appserver-io/appserver](https://github.com/appserver-io/appserver)
- [bernardphp/bernard](https://github.com/bernardphp/bernard)
- [florianv/swap](https://github.com/florianv/swap)
- [Dolibarr/dolibarr](https://github.com/Dolibarr/dolibarr)
- [Folkloreatelier/laravel-graphql](https://github.com/Folkloreatelier/laravel-graphql)
- [silexphp/Silex-Skeleton](https://github.com/silexphp/Silex-Skeleton)
- [FriendsOfSymfony/FOSJsRoutingBundle](https://github.com/FriendsOfSymfony/FOSJsRoutingBundle)
- [Pterodactyl/Panel](https://github.com/Pterodactyl/Panel)
- [spatie/laravel-fractal](https://github.com/spatie/laravel-fractal)
- [talyssonoc/react-laravel](https://github.com/talyssonoc/react-laravel)
- [phingofficial/phing](https://github.com/phingofficial/phing)
- [kahlan/kahlan](https://github.com/kahlan/kahlan)
- [lavary/crunz](https://github.com/lavary/crunz)
- [minkphp/Mink](https://github.com/minkphp/Mink)
- [katzgrau/KLogger](https://github.com/katzgrau/KLogger)
- [claviska/SimpleImage](https://github.com/claviska/SimpleImage)
- [spatie/browsershot](https://github.com/spatie/browsershot)
- [mikey179/vfsStream](https://github.com/mikey179/vfsStream)
- [Yoast/wordpress-seo](https://github.com/Yoast/wordpress-seo)
- [stof/StofDoctrineExtensionsBundle](https://github.com/stof/StofDoctrineExtensionsBundle)
- [croogo/croogo](https://github.com/croogo/croogo)
- [fxpio/composer-asset-plugin](https://github.com/fxpio/composer-asset-plugin)
- [iwind/rockmongo](https://github.com/iwind/rockmongo)
- [sabre-io/dav](https://github.com/sabre-io/dav)
- [vrana/notorm](https://github.com/vrana/notorm)
- [php-school/cli-menu](https://github.com/php-school/cli-menu)
- [opensourcepos/opensourcepos](https://github.com/opensourcepos/opensourcepos)
- [matthiasmullie/minify](https://github.com/matthiasmullie/minify)
- [willdurand/Hateoas](https://github.com/willdurand/Hateoas)
- [pinguo/php-msf](https://github.com/pinguo/php-msf)
- [jolicode/JoliNotif](https://github.com/jolicode/JoliNotif)
- [FriendsOfSymfony/FOSElasticaBundle](https://github.com/FriendsOfSymfony/FOSElasticaBundle)
- [bobthecow/Ruler](https://github.com/bobthecow/Ruler)
- [Froxlor/Froxlor](https://github.com/Froxlor/Froxlor)
- [amphp/aerys](https://github.com/amphp/aerys)
- [FriendsOfPHP/security-advisories](https://github.com/FriendsOfPHP/security-advisories)
- [sebastianfeldmann/phpbu](https://github.com/sebastianfeldmann/phpbu)
- [parse-community/parse-php-sdk](https://github.com/parse-community/parse-php-sdk)
- [codecasts/spa-starter-kit](https://github.com/codecasts/spa-starter-kit)
- [SegmentFault/HyperDown](https://github.com/SegmentFault/HyperDown)
- [technosophos/querypath](https://github.com/technosophos/querypath)
- [artesaos/seotools](https://github.com/artesaos/seotools)
- [benbalter/wordpress-to-jekyll-exporter](https://github.com/benbalter/wordpress-to-jekyll-exporter)
- [sebastianbergmann/php-code-coverage](https://github.com/sebastianbergmann/php-code-coverage)
- [Anahkiasen/underscore-php](https://github.com/Anahkiasen/underscore-php)
- [goodby/csv](https://github.com/goodby/csv)
- [dannyvankooten/AltoRouter](https://github.com/dannyvankooten/AltoRouter)
- [thephpleague/plates](https://github.com/thephpleague/plates)
- [LimeSurvey/LimeSurvey](https://github.com/LimeSurvey/LimeSurvey)
- [lexik/LexikJWTAuthenticationBundle](https://github.com/lexik/LexikJWTAuthenticationBundle)
- [doubleleft/hook](https://github.com/doubleleft/hook)
- [jwage/purl](https://github.com/jwage/purl)
- [liip/LiipImagineBundle](https://github.com/liip/LiipImagineBundle)
- [baijunyao/thinkphp-bjyadmin](https://github.com/baijunyao/thinkphp-bjyadmin)
- [amazonwebservices/aws-sdk-for-php](https://github.com/amazonwebservices/aws-sdk-for-php)
- [kristijanhusak/laravel-form-builder](https://github.com/kristijanhusak/laravel-form-builder)
- [ilya-dev/belt](https://github.com/ilya-dev/belt)
- [shaneharter/PHP-Daemon](https://github.com/shaneharter/PHP-Daemon)
- [laravel-zero/laravel-zero](https://github.com/laravel-zero/laravel-zero)
- [antonioribeiro/firewall](https://github.com/antonioribeiro/firewall)
- [whiteoctober/Pagerfanta](https://github.com/whiteoctober/Pagerfanta)
- [sendgrid/sendgrid-php](https://github.com/sendgrid/sendgrid-php)
- [shopware/shopware](https://github.com/shopware/shopware)
- [smalot/pdfparser](https://github.com/smalot/pdfparser)
- [noahbuscher/Macaw](https://github.com/noahbuscher/Macaw)
- [dwightwatson/validating](https://github.com/dwightwatson/validating)
- [cytopia/devilbox](https://github.com/cytopia/devilbox)
- [barbushin/php-imap](https://github.com/barbushin/php-imap)
- [Microsoft/msphpsql](https://github.com/Microsoft/msphpsql)
- [Automattic/jetpack](https://github.com/Automattic/jetpack)
- [wimg/PHPCompatibility](https://github.com/wimg/PHPCompatibility)
- [manifestinteractive/easyapns](https://github.com/manifestinteractive/easyapns)
- [niklasvh/php.js](https://github.com/niklasvh/php.js)
- [jenssegers/optimus](https://github.com/jenssegers/optimus)
- [openid/php-openid](https://github.com/openid/php-openid)
- [ant-vel/Antvel](https://github.com/ant-vel/Antvel)
- [fennb/phirehose](https://github.com/fennb/phirehose)
- [themosis/themosis](https://github.com/themosis/themosis)
- [dreamfactorysoftware/dreamfactory](https://github.com/dreamfactorysoftware/dreamfactory)
- [KnpLabs/KnpPaginatorBundle](https://github.com/KnpLabs/KnpPaginatorBundle)
- [cweiske/jsonmapper](https://github.com/cweiske/jsonmapper)
- [webpatser/laravel-uuid](https://github.com/webpatser/laravel-uuid)
- [someline/someline-starter](https://github.com/someline/someline-starter)
- [nikic/scalar_objects](https://github.com/nikic/scalar_objects)
- [jmathai/epiphany](https://github.com/jmathai/epiphany)
- [Neeke/SeasLog](https://github.com/Neeke/SeasLog)
- [netputer/wechat-php-sdk](https://github.com/netputer/wechat-php-sdk)
- [qieangel2013/zys](https://github.com/qieangel2013/zys)
- [jublonet/codebird-php](https://github.com/jublonet/codebird-php)
- [MrRio/shellwrap](https://github.com/MrRio/shellwrap)
- [jeremeamia/super_closure](https://github.com/jeremeamia/super_closure)
- [appzcoder/crud-generator](https://github.com/appzcoder/crud-generator)
- [opulencephp/Opulence](https://github.com/opulencephp/Opulence)
- [lyrixx/Silex-Kitchen-Edition](https://github.com/lyrixx/Silex-Kitchen-Edition)
- [hechoendrupal/drupal-console](https://github.com/hechoendrupal/drupal-console)
- [Roave/SecurityAdvisories](https://github.com/Roave/SecurityAdvisories)
- [mitulgolakiya/laravel-api-generator](https://github.com/mitulgolakiya/laravel-api-generator)
- [Xeoncross/micromvc](https://github.com/Xeoncross/micromvc)
- [bixuehujin/blink](https://github.com/bixuehujin/blink)
- [ircmaxell/PHPPHP](https://github.com/ircmaxell/PHPPHP)
- [sofadesign/limonade](https://github.com/sofadesign/limonade)
- [gantry/gantry5](https://github.com/gantry/gantry5)
- [ijry/lyadmin](https://github.com/ijry/lyadmin)
- [t0k4rt/phpqrcode](https://github.com/t0k4rt/phpqrcode)
- [snc/SncRedisBundle](https://github.com/snc/SncRedisBundle)
- [brianlmoon/GearmanManager](https://github.com/brianlmoon/GearmanManager)
- [ngfw/Recipe](https://github.com/ngfw/Recipe)
- [nategood/commando](https://github.com/nategood/commando)
- [Hifone/Hifone](https://github.com/Hifone/Hifone)
- [thephpleague/html-to-markdown](https://github.com/thephpleague/html-to-markdown)
- [pods-framework/pods](https://github.com/pods-framework/pods)
- [mewebstudio/Purifier](https://github.com/mewebstudio/Purifier)
- [fightbulc/moment.php](https://github.com/fightbulc/moment.php)
- [solariumphp/solarium](https://github.com/solariumphp/solarium)
- [santigarcor/laratrust](https://github.com/santigarcor/laratrust)
- [peej/tonic](https://github.com/peej/tonic)
- [Leafpub/leafpub](https://github.com/Leafpub/leafpub)
- [MenaraSolutions/geographer](https://github.com/MenaraSolutions/geographer)
- [johnbillion/query-monitor](https://github.com/johnbillion/query-monitor)
- [wordplate/wordplate](https://github.com/wordplate/wordplate)
- [franzliedke/studio](https://github.com/franzliedke/studio)
- [daylerees/scientist](https://github.com/daylerees/scientist)
- [php-pds/skeleton](https://github.com/php-pds/skeleton)
- [PHPOffice/PHPPresentation](https://github.com/PHPOffice/PHPPresentation)
- [bosnadev/repository](https://github.com/bosnadev/repository)
- [mauricesvay/php-facedetection](https://github.com/mauricesvay/php-facedetection)
- [phalcon/incubator](https://github.com/phalcon/incubator)
- [ktamas77/firebase-php](https://github.com/ktamas77/firebase-php)
- [FreshRSS/FreshRSS](https://github.com/FreshRSS/FreshRSS)
- [simshaun/recurr](https://github.com/simshaun/recurr)
- [oroinc/crm-application](https://github.com/oroinc/crm-application)
- [php-vcr/php-vcr](https://github.com/php-vcr/php-vcr)
- [backdrop/backdrop](https://github.com/backdrop/backdrop)
- [seblucas/cops](https://github.com/seblucas/cops)
- [pmmp/PocketMine-MP](https://github.com/pmmp/PocketMine-MP)
- [paragonie/halite](https://github.com/paragonie/halite)
- [garveen/laravoole](https://github.com/garveen/laravoole)
- [microweber/microweber](https://github.com/microweber/microweber)
- [ovr/phpsa](https://github.com/ovr/phpsa)
- [Gregwar/Image](https://github.com/Gregwar/Image)
- [jasny/sso](https://github.com/jasny/sso)
- [gimler/symfony-rest-edition](https://github.com/gimler/symfony-rest-edition)
- [KnpLabs/KnpSnappyBundle](https://github.com/KnpLabs/KnpSnappyBundle)
- [essence/essence](https://github.com/essence/essence)
- [mailgun/mailgun-php](https://github.com/mailgun/mailgun-php)
- [andres-montanez/Magallanes](https://github.com/andres-montanez/Magallanes)
- [Gregwar/Captcha](https://github.com/Gregwar/Captcha)
- [phansible/phansible](https://github.com/phansible/phansible)
- [wsdl2phpgenerator/wsdl2phpgenerator](https://github.com/wsdl2phpgenerator/wsdl2phpgenerator)
- [ghedipunk/PHP-Websockets](https://github.com/ghedipunk/PHP-Websockets)
- [Cilex/Cilex](https://github.com/Cilex/Cilex)
- [EnMarche/en-marche.fr](https://github.com/EnMarche/en-marche.fr)
- [bshaffer/oauth2-demo-php](https://github.com/bshaffer/oauth2-demo-php)
- [easydigitaldownloads/easy-digital-downloads](https://github.com/easydigitaldownloads/easy-digital-downloads)
- [jae-jae/QueryList](https://github.com/jae-jae/QueryList)
- [orchestral/testbench](https://github.com/orchestral/testbench)
- [JBZoo/Utils](https://github.com/JBZoo/Utils)
- [EleTeam/Shop-PHP-Yii2](https://github.com/EleTeam/Shop-PHP-Yii2)
- [allegro/php-protobuf](https://github.com/allegro/php-protobuf)
- [yupe/yupe](https://github.com/yupe/yupe)
- [morrisonlevi/Ardent](https://github.com/morrisonlevi/Ardent)
- [kosinix/grafika](https://github.com/kosinix/grafika)
- [sektioneins/pcc](https://github.com/sektioneins/pcc)
- [CoderKungfu/php-queue](https://github.com/CoderKungfu/php-queue)
- [spatie/blender](https://github.com/spatie/blender)
- [Program-O/Program-O](https://github.com/Program-O/Program-O)
- [spatie/laravel-newsletter](https://github.com/spatie/laravel-newsletter)
- [phpbench/phpbench](https://github.com/phpbench/phpbench)
- [kriswallsmith/spork](https://github.com/kriswallsmith/spork)
- [sulu/sulu-standard](https://github.com/sulu/sulu-standard)
- [igorw/evenement](https://github.com/igorw/evenement)
- [kbjr/Git.php](https://github.com/kbjr/Git.php)
- [phalcon/mvc](https://github.com/phalcon/mvc)
- [REBELinBLUE/deployer](https://github.com/REBELinBLUE/deployer)
- [TheOrchid/Platform](https://github.com/TheOrchid/Platform)
- [PrivateBin/PrivateBin](https://github.com/PrivateBin/PrivateBin)
- [openemr/openemr](https://github.com/openemr/openemr)
- [PHPIDS/PHPIDS](https://github.com/PHPIDS/PHPIDS)
- [emoncms/emoncms](https://github.com/emoncms/emoncms)
- [K-Phoen/rulerz](https://github.com/K-Phoen/rulerz)
- [BenExile/Dropbox](https://github.com/BenExile/Dropbox)
- [DevGroup-ru/dotplant2](https://github.com/DevGroup-ru/dotplant2)
- [weiboad/kafka-php](https://github.com/weiboad/kafka-php)
- [clarkeash/doorman](https://github.com/clarkeash/doorman)
- [movim/movim](https://github.com/movim/movim)
- [phayes/geoPHP](https://github.com/phayes/geoPHP)
- [envms/fluentpdo](https://github.com/envms/fluentpdo)
- [KnpLabs/KnpMenuBundle](https://github.com/KnpLabs/KnpMenuBundle)
- [QafooLabs/php-refactoring-browser](https://github.com/QafooLabs/php-refactoring-browser)
- [phpipam/phpipam](https://github.com/phpipam/phpipam)
- [getsentry/sentry-php](https://github.com/getsentry/sentry-php)
- [Exeu/apai-io](https://github.com/Exeu/apai-io)
- [hassankhan/config](https://github.com/hassankhan/config)
- [twigphp/Twig-extensions](https://github.com/twigphp/Twig-extensions)
- [mike42/escpos-php](https://github.com/mike42/escpos-php)
- [fethica/PHP-Login](https://github.com/fethica/PHP-Login)
- [SimpleSoftwareIO/simple-qrcode](https://github.com/SimpleSoftwareIO/simple-qrcode)
- [mongodb/mongo-php-library](https://github.com/mongodb/mongo-php-library)
- [chrisboulton/php-diff](https://github.com/chrisboulton/php-diff)
- [jadell/neo4jphp](https://github.com/jadell/neo4jphp)
- [easychen/LazyPHP](https://github.com/easychen/LazyPHP)
- [contao/core](https://github.com/contao/core)
- [phpfunct/funct](https://github.com/phpfunct/funct)
- [victorstanciu/Wikitten](https://github.com/victorstanciu/Wikitten)
- [CodeSleeve/stapler](https://github.com/CodeSleeve/stapler)
- [wp-cli/php-cli-tools](https://github.com/wp-cli/php-cli-tools)
- [wickyaswal/indieteq-php-my-sql-pdo-database-class](https://github.com/wickyaswal/indieteq-php-my-sql-pdo-database-class)
- [schmittjoh/php-option](https://github.com/schmittjoh/php-option)
- [bmitch/churn-php](https://github.com/bmitch/churn-php)
- [anhskohbo/no-captcha](https://github.com/anhskohbo/no-captcha)
- [giorgiosironi/phpunit-selenium](https://github.com/giorgiosironi/phpunit-selenium)
- [peteboere/css-crush](https://github.com/peteboere/css-crush)
- [jbroadway/urlify](https://github.com/jbroadway/urlify)
- [phoronix-test-suite/phoronix-test-suite](https://github.com/phoronix-test-suite/phoronix-test-suite)
- [commerceguys/addressing](https://github.com/commerceguys/addressing)
- [symphonycms/symphony-2](https://github.com/symphonycms/symphony-2)
- [mdkholy/dashbrew](https://github.com/mdkholy/dashbrew)
- [Youshido/GraphQL](https://github.com/Youshido/GraphQL)
- [spatie/laravel-responsecache](https://github.com/spatie/laravel-responsecache)
- [walkor/shadowsocks-php](https://github.com/walkor/shadowsocks-php)
- [jeckman/YouTube-Downloader](https://github.com/jeckman/YouTube-Downloader)
- [docker-php/docker-php](https://github.com/docker-php/docker-php)
- [analogueorm/analogue](https://github.com/analogueorm/analogue)
- [clue/graph-composer](https://github.com/clue/graph-composer)
- [walkor/web-msg-sender](https://github.com/walkor/web-msg-sender)
- [paragonie/random_compat](https://github.com/paragonie/random_compat)
- [jaysalvat/image2css](https://github.com/jaysalvat/image2css)
- [api-platform/core](https://github.com/api-platform/core)
- [sensiolabs/security-checker](https://github.com/sensiolabs/security-checker)
- [qiniu/php-sdk](https://github.com/qiniu/php-sdk)
- [AlloVince/EvaThumber](https://github.com/AlloVince/EvaThumber)
- [ifsnop/mysqldump-php](https://github.com/ifsnop/mysqldump-php)
- [noodlehaus/dispatch](https://github.com/noodlehaus/dispatch)
- [alextselegidis/easyappointments](https://github.com/alextselegidis/easyappointments)
- [OpenMage/magento-mirror](https://github.com/OpenMage/magento-mirror)
- [craue/CraueFormFlowBundle](https://github.com/craue/CraueFormFlowBundle)
- [Alexia/php7mar](https://github.com/Alexia/php7mar)
- [msgpack/msgpack-php](https://github.com/msgpack/msgpack-php)
- [TYPO3/TYPO3.CMS](https://github.com/TYPO3/TYPO3.CMS)
- [virtphp/virtphp](https://github.com/virtphp/virtphp)
- [usmanhalalit/pixie](https://github.com/usmanhalalit/pixie)
- [myclabs/php-enum](https://github.com/myclabs/php-enum)
- [nexcess/magento-turpentine](https://github.com/nexcess/magento-turpentine)
- [Chassis/Chassis](https://github.com/Chassis/Chassis)
- [beberlei/litecqrs-php](https://github.com/beberlei/litecqrs-php)
- [toplan/phpsms](https://github.com/toplan/phpsms)
- [feelinglucky/php-readability](https://github.com/feelinglucky/php-readability)
- [tedious/JShrink](https://github.com/tedious/JShrink)
- [ronanguilloux/IsoCodes](https://github.com/ronanguilloux/IsoCodes)
- [Pawka/phrozn](https://github.com/Pawka/phrozn)
- [ruckus/ruckusing-migrations](https://github.com/ruckus/ruckusing-migrations)
- [Bee-Lab/bowerphp](https://github.com/Bee-Lab/bowerphp)
- [recoilphp/recoil](https://github.com/recoilphp/recoil)
- [iliaal/php_excel](https://github.com/iliaal/php_excel)
- [BOINC/boinc](https://github.com/BOINC/boinc)
- [bruli/php-git-hooks](https://github.com/bruli/php-git-hooks)
- [php-enqueue/enqueue-dev](https://github.com/php-enqueue/enqueue-dev)
- [mnapoli/silly](https://github.com/mnapoli/silly)
- [firefly-iii/firefly-iii](https://github.com/firefly-iii/firefly-iii)
- [webtechnick/CakePHP-Facebook-Plugin](https://github.com/webtechnick/CakePHP-Facebook-Plugin)
- [mk-j/PHP_XLSXWriter](https://github.com/mk-j/PHP_XLSXWriter)
- [pusher/pusher-http-php](https://github.com/pusher/pusher-http-php)
- [spatie/regex](https://github.com/spatie/regex)
- [varspool/Wrench](https://github.com/varspool/Wrench)
- [mysql-workbench-schema-exporter/mysql-workbench-schema-exporter](https://github.com/mysql-workbench-schema-exporter/mysql-workbench-schema-exporter)
- [mrjgreen/phroute](https://github.com/mrjgreen/phroute)
- [appstract/laravel-opcache](https://github.com/appstract/laravel-opcache)
- [allynbauer/statuspanic](https://github.com/allynbauer/statuspanic)
- [phalapi/phalapi](https://github.com/phalapi/phalapi)
- [Microsoft/tolerant-php-parser](https://github.com/Microsoft/tolerant-php-parser)
- [web-push-libs/web-push-php](https://github.com/web-push-libs/web-push-php)
- [clickalicious/phpmemadmin](https://github.com/clickalicious/phpmemadmin)
- [thephpleague/shunt](https://github.com/thephpleague/shunt)
- [KnpLabs/KnpMenu](https://github.com/KnpLabs/KnpMenu)
- [amranidev/scaffold-interface](https://github.com/amranidev/scaffold-interface)
- [niutech/node.php](https://github.com/niutech/node.php)
- [tschoffelen/PHP-PKPass](https://github.com/tschoffelen/PHP-PKPass)
- [impresspages/ImpressPages](https://github.com/impresspages/ImpressPages)
- [everzet/jade.php](https://github.com/everzet/jade.php)
- [dannyvankooten/PHP-Router](https://github.com/dannyvankooten/PHP-Router)
- [PHPAuth/PHPAuth](https://github.com/PHPAuth/PHPAuth)
- [asimlqt/php-google-spreadsheet-client](https://github.com/asimlqt/php-google-spreadsheet-client)
- [namshi/jose](https://github.com/namshi/jose)
- [spipu/html2pdf](https://github.com/spipu/html2pdf)
- [FriendsOfPHP/uprofiler](https://github.com/FriendsOfPHP/uprofiler)
- [jeremykendall/php-domain-parser](https://github.com/jeremykendall/php-domain-parser)
- [davedevelopment/phpmig](https://github.com/davedevelopment/phpmig)
- [TankAuth/Tank-Auth](https://github.com/TankAuth/Tank-Auth)
- [patrikf/glip](https://github.com/patrikf/glip)
- [YetiForceCompany/YetiForceCRM](https://github.com/YetiForceCompany/YetiForceCRM)
- [vimeo/psalm](https://github.com/vimeo/psalm)
- [TIGERB/easy-php](https://github.com/TIGERB/easy-php)
- [iTXTech/Genisys](https://github.com/iTXTech/Genisys)
- [mustangostang/spyc](https://github.com/mustangostang/spyc)
- [MiniCodeMonkey/Vagrant-LAMP-Stack](https://github.com/MiniCodeMonkey/Vagrant-LAMP-Stack)
- [angeloskath/php-nlp-tools](https://github.com/angeloskath/php-nlp-tools)
- [nixsolutions/yandex-php-library](https://github.com/nixsolutions/yandex-php-library)
- [chakhsu/pinghsu](https://github.com/chakhsu/pinghsu)
- [willdurand/EmailReplyParser](https://github.com/willdurand/EmailReplyParser)
- [raulfraile/ladybug](https://github.com/raulfraile/ladybug)
- [clue/phar-composer](https://github.com/clue/phar-composer)
- [timegridio/timegrid](https://github.com/timegridio/timegrid)
- [tedious/Fetch](https://github.com/tedious/Fetch)
- [dwightwatson/rememberable](https://github.com/dwightwatson/rememberable)
- [intaro/pinboard](https://github.com/intaro/pinboard)
- [Seldaek/php-console](https://github.com/Seldaek/php-console)
- [NauxLiu/phphub-server](https://github.com/NauxLiu/phphub-server)
- [symfony/console](https://github.com/symfony/console)
- [microweber/screen](https://github.com/microweber/screen)
- [felixfbecker/php-language-server](https://github.com/felixfbecker/php-language-server)
- [akeneo/pim-community-dev](https://github.com/akeneo/pim-community-dev)
- [Fixhub/Fixhub](https://github.com/Fixhub/Fixhub)
- [devster/ubench](https://github.com/devster/ubench)
- [tylerhall/simple-php-framework](https://github.com/tylerhall/simple-php-framework)
- [simplesamlphp/simplesamlphp](https://github.com/simplesamlphp/simplesamlphp)
- [rgrove/jsmin-php](https://github.com/rgrove/jsmin-php)
- [jacwright/RestServer](https://github.com/jacwright/RestServer)
- [voryx/Thruway](https://github.com/voryx/Thruway)
- [mybb/mybb](https://github.com/mybb/mybb)
- [emposha/PHP-Shell-Detector](https://github.com/emposha/PHP-Shell-Detector)
- [apereo/phpCAS](https://github.com/apereo/phpCAS)
- [gajus/xhprof.io](https://github.com/gajus/xhprof.io)
- [Roave/BetterReflection](https://github.com/Roave/BetterReflection)
- [gorhill/PHP-FineDiff](https://github.com/gorhill/PHP-FineDiff)
- [fukuball/jieba-php](https://github.com/fukuball/jieba-php)
- [DirectoryLister/DirectoryLister](https://github.com/DirectoryLister/DirectoryLister)
- [thibaud-rohmer/PhotoShow](https://github.com/thibaud-rohmer/PhotoShow)
- [laracasts/TestDummy](https://github.com/laracasts/TestDummy)
- [panique/php-login-minimal](https://github.com/panique/php-login-minimal)
- [onelogin/php-saml](https://github.com/onelogin/php-saml)
- [m4tthumphrey/php-gitlab-api](https://github.com/m4tthumphrey/php-gitlab-api)
- [JayBizzle/Crawler-Detect](https://github.com/JayBizzle/Crawler-Detect)
- [Rudloff/alltube](https://github.com/Rudloff/alltube)
- [lastguest/pixeler](https://github.com/lastguest/pixeler)
- [1up-lab/OneupUploaderBundle](https://github.com/1up-lab/OneupUploaderBundle)
- [faisalman/simple-excel-php](https://github.com/faisalman/simple-excel-php)
- [fabfuel/prophiler](https://github.com/fabfuel/prophiler)
- [certificationy/certificationy](https://github.com/certificationy/certificationy)
- [spatie/laravel-uptime-monitor](https://github.com/spatie/laravel-uptime-monitor)
- [nielse63/php-image-cache](https://github.com/nielse63/php-image-cache)
- [bastianallgeier/gantti](https://github.com/bastianallgeier/gantti)
- [Frug/AJAX-Chat](https://github.com/Frug/AJAX-Chat)
- [miniflux/picoFeed](https://github.com/miniflux/picoFeed)
- [mongodb/mongo-php-driver](https://github.com/mongodb/mongo-php-driver)
- [laravolt/avatar](https://github.com/laravolt/avatar)
- [jamesiarmes/php-ews](https://github.com/jamesiarmes/php-ews)
- [dotcppfile/DAws](https://github.com/dotcppfile/DAws)
- [walkor/workerman-chat](https://github.com/walkor/workerman-chat)
- [Quixotix/PHP-PayPal-IPN](https://github.com/Quixotix/PHP-PayPal-IPN)
- [dapphp/securimage](https://github.com/dapphp/securimage)
- [clue/graph](https://github.com/clue/graph)
- [nikic/php-ast](https://github.com/nikic/php-ast)
- [maghead/maghead](https://github.com/maghead/maghead)
- [upwork/phystrix](https://github.com/upwork/phystrix)
- [theseer/phpdox](https://github.com/theseer/phpdox)
- [nova-framework/framework](https://github.com/nova-framework/framework)
- [kiddyuchina/Beanbun](https://github.com/kiddyuchina/Beanbun)
- [zordius/lightncandy](https://github.com/zordius/lightncandy)
- [rackspace/php-opencloud](https://github.com/rackspace/php-opencloud)
- [nZEDb/nZEDb](https://github.com/nZEDb/nZEDb)
- [luyadev/luya](https://github.com/luyadev/luya)
- [jrean/laravel-user-verification](https://github.com/jrean/laravel-user-verification)
- [GaretJax/phpbrowscap](https://github.com/GaretJax/phpbrowscap)
- [yohang/CalendR](https://github.com/yohang/CalendR)
- [themosis/framework](https://github.com/themosis/framework)
- [hoaproject/Ruler](https://github.com/hoaproject/Ruler)
- [drslump/Protobuf-PHP](https://github.com/drslump/Protobuf-PHP)
- [object-calisthenics/phpcs-calisthenics-rules](https://github.com/object-calisthenics/phpcs-calisthenics-rules)
- [mlively/Phake](https://github.com/mlively/Phake)
- [concrete5/concrete5](https://github.com/concrete5/concrete5)
- [jcampbell1/simple-file-manager](https://github.com/jcampbell1/simple-file-manager)
- [xcl3721/Dora-RPC](https://github.com/xcl3721/Dora-RPC)
- [willdurand/Negotiation](https://github.com/willdurand/Negotiation)
- [nelmio/NelmioCorsBundle](https://github.com/nelmio/NelmioCorsBundle)
- [APY/APYDataGridBundle](https://github.com/APY/APYDataGridBundle)
- [panique/mini2](https://github.com/panique/mini2)
- [AsgardCms/Platform](https://github.com/AsgardCms/Platform)
- [xPaw/PHP-Minecraft-Query](https://github.com/xPaw/PHP-Minecraft-Query)
- [Spomky-Labs/otphp](https://github.com/Spomky-Labs/otphp)
- [Openovate/eden](https://github.com/Openovate/eden)
- [toin0u/DigitalOceanV2](https://github.com/toin0u/DigitalOceanV2)
- [tecnickcom/tc-lib-pdf](https://github.com/tecnickcom/tc-lib-pdf)
- [symfony/dom-crawler](https://github.com/symfony/dom-crawler)
- [wapmorgan/Morphos](https://github.com/wapmorgan/Morphos)
- [auraphp/Aura.Sql](https://github.com/auraphp/Aura.Sql)
- [ericmakesstuff/laravel-server-monitor](https://github.com/ericmakesstuff/laravel-server-monitor)
- [maxmind/geoip-api-php](https://github.com/maxmind/geoip-api-php)
- [woocommerce/storefront](https://github.com/woocommerce/storefront)
- [topdown/phpStorm-CC-Helpers](https://github.com/topdown/phpStorm-CC-Helpers)
- [marcioAlmada/yay](https://github.com/marcioAlmada/yay)
- [LoeiFy/Diaspora](https://github.com/LoeiFy/Diaspora)
- [TimeToogo/Pinq](https://github.com/TimeToogo/Pinq)
- [radiosilence/Ham](https://github.com/radiosilence/Ham)
- [spatie/laravel-url-signer](https://github.com/spatie/laravel-url-signer)
- [potsky/PimpMyLog](https://github.com/potsky/PimpMyLog)
- [php-http/httplug](https://github.com/php-http/httplug)
- [livestreet/livestreet](https://github.com/livestreet/livestreet)
- [spatie/image-optimizer](https://github.com/spatie/image-optimizer)
- [FriendsOfSymfony/FOSCommentBundle](https://github.com/FriendsOfSymfony/FOSCommentBundle)
- [azuyalabs/yasumi](https://github.com/azuyalabs/yasumi)
- [postaddictme/instagram-php-scraper](https://github.com/postaddictme/instagram-php-scraper)
- [jaxl/JAXL](https://github.com/jaxl/JAXL)
- [uxweb/sweet-alert](https://github.com/uxweb/sweet-alert)
- [RaymiiOrg/ssl-decoder](https://github.com/RaymiiOrg/ssl-decoder)
- [bergie/dnode-php](https://github.com/bergie/dnode-php)
- [eventviva/php-image-resize](https://github.com/eventviva/php-image-resize)
- [Cacti/cacti](https://github.com/Cacti/cacti)
- [bjeavons/zxcvbn-php](https://github.com/bjeavons/zxcvbn-php)
- [pyrech/composer-changelogs](https://github.com/pyrech/composer-changelogs)
- [ircmaxell/filterus](https://github.com/ircmaxell/filterus)
- [tlhunter/neoinvoice](https://github.com/tlhunter/neoinvoice)
- [liip/LiipFunctionalTestBundle](https://github.com/liip/LiipFunctionalTestBundle)
- [cakephp/chronos](https://github.com/cakephp/chronos)
- [jaz303/phake](https://github.com/jaz303/phake)
- [spatie/opening-hours](https://github.com/spatie/opening-hours)
- [kronusme/dota2-api](https://github.com/kronusme/dota2-api)
- [spatie/laravel-collection-macros](https://github.com/spatie/laravel-collection-macros)
- [thirtybees/thirtybees](https://github.com/thirtybees/thirtybees)
- [Stichoza/google-translate-php](https://github.com/Stichoza/google-translate-php)
- [phpcr/phpcr](https://github.com/phpcr/phpcr)
- [nuovo/spreadsheet-reader](https://github.com/nuovo/spreadsheet-reader)
- [caoym/phpboot](https://github.com/caoym/phpboot)
- [shuber/curl](https://github.com/shuber/curl)
- [commando/dogpatch](https://github.com/commando/dogpatch)
- [bupt1987/html-parser](https://github.com/bupt1987/html-parser)
- [dg/ftp-deployment](https://github.com/dg/ftp-deployment)
- [verot/class.upload.php](https://github.com/verot/class.upload.php)
- [hoaproject/Websocket](https://github.com/hoaproject/Websocket)
- [amphp/artax](https://github.com/amphp/artax)
- [tomzx/php-semver-checker](https://github.com/tomzx/php-semver-checker)
- [stefanzweifel/laravel-stats](https://github.com/stefanzweifel/laravel-stats)
- [patrickschur/language-detection](https://github.com/patrickschur/language-detection)
- [matteosister/GitElephant](https://github.com/matteosister/GitElephant)
- [cbschuld/Browser.php](https://github.com/cbschuld/Browser.php)
- [spatie/laravel-translatable](https://github.com/spatie/laravel-translatable)
- [sentora/sentora-core](https://github.com/sentora/sentora-core)
- [Ocramius/GeneratedHydrator](https://github.com/Ocramius/GeneratedHydrator)
- [CobreGratis/boletophp](https://github.com/CobreGratis/boletophp)
- [appstract/laravel-blade-directives](https://github.com/appstract/laravel-blade-directives)
- [fenom-template/fenom](https://github.com/fenom-template/fenom)
- [ksubileau/color-thief-php](https://github.com/ksubileau/color-thief-php)
- [kevinkhill/lavacharts](https://github.com/kevinkhill/lavacharts)
- [hbattat/verifyEmail](https://github.com/hbattat/verifyEmail)
- [sabberworm/PHP-CSS-Parser](https://github.com/sabberworm/PHP-CSS-Parser)
- [malkusch/lock](https://github.com/malkusch/lock)
- [markstory/asset_compress](https://github.com/markstory/asset_compress)
- [jitamin/jitamin](https://github.com/jitamin/jitamin)
- [jasonmunro/cypht](https://github.com/jasonmunro/cypht)
- [ircmaxell/PHP-PasswordLib](https://github.com/ircmaxell/PHP-PasswordLib)
- [thorsten/phpMyFAQ](https://github.com/thorsten/phpMyFAQ)
- [mattiasgeniar/php-exploit-scripts](https://github.com/mattiasgeniar/php-exploit-scripts)
- [parsecsv/parsecsv-for-php](https://github.com/parsecsv/parsecsv-for-php)
- [GoogleCloudPlatform/appengine-php-wordpress-starter-project](https://github.com/GoogleCloudPlatform/appengine-php-wordpress-starter-project)
- [opencfp/opencfp](https://github.com/opencfp/opencfp)
- [jasonhinkle/phreeze](https://github.com/jasonhinkle/phreeze)
- [tchwork/utf8](https://github.com/tchwork/utf8)
- [educoder/pest](https://github.com/educoder/pest)
- [bocharsky-bw/Arrayzy](https://github.com/bocharsky-bw/Arrayzy)
- [BadChoice/handesk](https://github.com/BadChoice/handesk)
- [antonioribeiro/ci](https://github.com/antonioribeiro/ci)
- [symfony/http-foundation](https://github.com/symfony/http-foundation)
- [paragonie/csp-builder](https://github.com/paragonie/csp-builder)
- [paragonie/airship](https://github.com/paragonie/airship)
- [adoy/PHP-OAuth2](https://github.com/adoy/PHP-OAuth2)
- [shadowhand/latitude](https://github.com/shadowhand/latitude)
- [jp7internet/laravel-apz](https://github.com/jp7internet/laravel-apz)
- [timber/starter-theme](https://github.com/timber/starter-theme)
- [GeniusesOfSymfony/WebSocketBundle](https://github.com/GeniusesOfSymfony/WebSocketBundle)
- [sabre-io/vobject](https://github.com/sabre-io/vobject)
- [guzzle/promises](https://github.com/guzzle/promises)
- [sinergi/php-browser-detector](https://github.com/sinergi/php-browser-detector)
- [PavelLoparev/design-patterns](https://github.com/PavelLoparev/design-patterns)
- [adldap/adLDAP](https://github.com/adldap/adLDAP)
- [sensiolabs/melody](https://github.com/sensiolabs/melody)
- [sebastianbergmann/phpdcd](https://github.com/sebastianbergmann/phpdcd)
- [hautelook/AliceBundle](https://github.com/hautelook/AliceBundle)
- [rodneyrehm/CFPropertyList](https://github.com/rodneyrehm/CFPropertyList)
- [ramsey/array_column](https://github.com/ramsey/array_column)
- [markuspoerschke/iCal](https://github.com/markuspoerschke/iCal)
- [jenssegers/php-proxy](https://github.com/jenssegers/php-proxy)
- [GitaminHQ/Gitamin](https://github.com/GitaminHQ/Gitamin)
- [raulfraile/LadybugBundle](https://github.com/raulfraile/LadybugBundle)
- [DusanKasan/Knapsack](https://github.com/DusanKasan/Knapsack)
- [arnaud-lb/MtHaml](https://github.com/arnaud-lb/MtHaml)
- [Trismegiste/Mondrian](https://github.com/Trismegiste/Mondrian)
- [memio/memio](https://github.com/memio/memio)
- [tumblr/tumblr.php](https://github.com/tumblr/tumblr.php)
- [php/web-php](https://github.com/php/web-php)
- [ornicar/php-github-api](https://github.com/ornicar/php-github-api)
- [galen/PHP-Instagram-API](https://github.com/galen/PHP-Instagram-API)
- [nette/latte](https://github.com/nette/latte)
- [joshdick/miniProxy](https://github.com/joshdick/miniProxy)
- [dg/twitter-php](https://github.com/dg/twitter-php)
- [zpanel/zpanelx](https://github.com/zpanel/zpanelx)
- [vlucas/bulletphp](https://github.com/vlucas/bulletphp)
- [thephpleague/url](https://github.com/thephpleague/url)
- [redmatrix/hubzilla](https://github.com/redmatrix/hubzilla)
- [tokudu/PhpMQTTClient](https://github.com/tokudu/PhpMQTTClient)
- [php-coveralls/php-coveralls](https://github.com/php-coveralls/php-coveralls)
- [oleksandr-torosh/yona-cms](https://github.com/oleksandr-torosh/yona-cms)
- [maciejczyzewski/bottomline](https://github.com/maciejczyzewski/bottomline)
- [KnpLabs/KnpGaufretteBundle](https://github.com/KnpLabs/KnpGaufretteBundle)
- [weprovide/valet-plus](https://github.com/weprovide/valet-plus)
- [engintron/engintron](https://github.com/engintron/engintron)
- [auraphp/Aura.Router](https://github.com/auraphp/Aura.Router)
- [afterlogic/webmail-lite](https://github.com/afterlogic/webmail-lite)
- [sebastiaanluca/laravel-helpers](https://github.com/sebastiaanluca/laravel-helpers)
- [PUGX/badge-poser](https://github.com/PUGX/badge-poser)
- [travis-ci-examples/php](https://github.com/travis-ci-examples/php)
- [psecio/gatekeeper](https://github.com/psecio/gatekeeper)
- [ezimuel/PHP-Secure-Session](https://github.com/ezimuel/PHP-Secure-Session)
- [sonata-project/SonataMediaBundle](https://github.com/sonata-project/SonataMediaBundle)
- [JetBrains/phpstorm-stubs](https://github.com/JetBrains/phpstorm-stubs)
- [PuShaoWei/arithmetic-php](https://github.com/PuShaoWei/arithmetic-php)
- [p-h-p/instagraph](https://github.com/p-h-p/instagraph)
- [sleimanx2/plastic](https://github.com/sleimanx2/plastic)
- [petewarden/ParallelCurl](https://github.com/petewarden/ParallelCurl)
- [pascaldevink/shortuuid](https://github.com/pascaldevink/shortuuid)
- [kenjis/ci-phpunit-test](https://github.com/kenjis/ci-phpunit-test)
- [fguillot/JsonRPC](https://github.com/fguillot/JsonRPC)
- [EC-CUBE/ec-cube](https://github.com/EC-CUBE/ec-cube)
- [Webschool-io/Curso-PHP-Laravel-Completo-E-Total](https://github.com/Webschool-io/Curso-PHP-Laravel-Completo-E-Total)
- [googleads/googleads-php-lib](https://github.com/googleads/googleads-php-lib)
- [antecedent/patchwork](https://github.com/antecedent/patchwork)
- [liip/LiipMonitorBundle](https://github.com/liip/LiipMonitorBundle)
- [jmolivas/phpqa](https://github.com/jmolivas/phpqa)
- [XaminProject/handlebars.php](https://github.com/XaminProject/handlebars.php)
- [php-mime-mail-parser/php-mime-mail-parser](https://github.com/php-mime-mail-parser/php-mime-mail-parser)
- [oscarotero/Gettext](https://github.com/oscarotero/Gettext)
- [orchestral/tenanti](https://github.com/orchestral/tenanti)
- [hannob/php-crashers](https://github.com/hannob/php-crashers)
- [reactphp/react](https://github.com/reactphp/react)
- [renatomarinho/laravel-gitscrum](https://github.com/renatomarinho/laravel-gitscrum)
- [api-platform/api-platform](https://github.com/api-platform/api-platform)
- [Mashape/unirest-php](https://github.com/Mashape/unirest-php)
- [symfony/symfony-demo](https://github.com/symfony/symfony-demo)
- [fruux/sabre-dav](https://github.com/fruux/sabre-dav)
- [nfephp-org/nfephp](https://github.com/nfephp-org/nfephp)
- [notadd/notadd](https://github.com/notadd/notadd)
- [fruux/sabre-vobject](https://github.com/fruux/sabre-vobject)
- [jjgrainger/wp-custom-post-type-class](https://github.com/jjgrainger/wp-custom-post-type-class)
- [nazariyg/Phred](https://github.com/nazariyg/Phred)
- [Vectorface/whip](https://github.com/Vectorface/whip)
- [TinyLara/TinyLara](https://github.com/TinyLara/TinyLara)
- [selvinortiz/flux](https://github.com/selvinortiz/flux)
- [morozovsk/websocket](https://github.com/morozovsk/websocket)
- [ghunti/HighchartsPHP](https://github.com/ghunti/HighchartsPHP)
- [nervetattoo/elasticsearch](https://github.com/nervetattoo/elasticsearch)
- [tobscure/json-api](https://github.com/tobscure/json-api)
- [tackk/cartographer](https://github.com/tackk/cartographer)
- [jekkos/opensourcepos](https://github.com/jekkos/opensourcepos)
- [stephens2424/php](https://github.com/stephens2424/php)
- [crisu83/yiistrap](https://github.com/crisu83/yiistrap)
- [spress/Spress](https://github.com/spress/Spress)
- [snytkine/LampCMS](https://github.com/snytkine/LampCMS)
- [PufferPanel/PufferPanel](https://github.com/PufferPanel/PufferPanel)
- [phprest/phprest](https://github.com/phprest/phprest)
- [php-libs/JsonRPC](https://github.com/php-libs/JsonRPC)
- [c9s/CLIFramework](https://github.com/c9s/CLIFramework)
- [a1phanumeric/PHP-MySQL-Class](https://github.com/a1phanumeric/PHP-MySQL-Class)
- [polyfractal/athletic](https://github.com/polyfractal/athletic)
- [kbsali/php-redmine-api](https://github.com/kbsali/php-redmine-api)
- [JakubOnderka/PHP-Parallel-Lint](https://github.com/JakubOnderka/PHP-Parallel-Lint)
- [florianv/business](https://github.com/florianv/business)
- [Level-2/Dice](https://github.com/Level-2/Dice)
- [EasyCorp/easy-log-handler](https://github.com/EasyCorp/easy-log-handler)
- [etsy/phan](https://github.com/etsy/phan)
- [GitScrum-Community/laravel-gitscrum](https://github.com/GitScrum-Community/laravel-gitscrum)
- [Masterminds/html5-php](https://github.com/Masterminds/html5-php)
- [nunomaduro/laravel-zero](https://github.com/nunomaduro/laravel-zero)
- [satooshi/php-coveralls](https://github.com/satooshi/php-coveralls)
- [tylerhall/sosumi](https://github.com/tylerhall/sosumi)
- [Schepp/CSS-JS-Booster](https://github.com/Schepp/CSS-JS-Booster)
- [indeyets/appserver-in-php](https://github.com/indeyets/appserver-in-php)
- [qandidate-labs/qandidate-toggle](https://github.com/qandidate-labs/qandidate-toggle)
- [artesaos/defender](https://github.com/artesaos/defender)
- [gabrielbull/omnimail](https://github.com/gabrielbull/omnimail)
- [thomashempel/AlfredGoogleTranslateWorkflow](https://github.com/thomashempel/AlfredGoogleTranslateWorkflow)
- [symfony/symfony-installer](https://github.com/symfony/symfony-installer)
- [khanamiryan/php-qrcode-detector-decoder](https://github.com/khanamiryan/php-qrcode-detector-decoder)
- [anantgarg/Qwench](https://github.com/anantgarg/Qwench)
- [servo-php/fluidxml](https://github.com/servo-php/fluidxml)
- [orocrm/crm-application](https://github.com/orocrm/crm-application)
- [sendya/shadowsocks-panel](https://github.com/sendya/shadowsocks-panel)
- [tuupola/slim-jwt-auth](https://github.com/tuupola/slim-jwt-auth)
- [Tuhinshubhra/RED_HAWK](https://github.com/Tuhinshubhra/RED_HAWK)
- [EcomDev/EcomDev_PHPUnit](https://github.com/EcomDev/EcomDev_PHPUnit)
- [hollodotme/Helpers](https://github.com/hollodotme/Helpers)
- [robclancy/presenter](https://github.com/robclancy/presenter)
- [crodas/LanguageDetector](https://github.com/crodas/LanguageDetector)
- [jmathai/php-multi-curl](https://github.com/jmathai/php-multi-curl)
- [WhichBrowser/Parser](https://github.com/WhichBrowser/Parser)
- [zhiyicx/thinksns-plus](https://github.com/zhiyicx/thinksns-plus)
- [Jasig/phpCAS](https://github.com/Jasig/phpCAS)
- [apsdehal/Link](https://github.com/apsdehal/Link)
- [psliwa/PHPPdf](https://github.com/psliwa/PHPPdf)
- [mexitek/phpColors](https://github.com/mexitek/phpColors)
- [adlawson/php-vfs](https://github.com/adlawson/php-vfs)
- [thomasbachem/php-ga](https://github.com/thomasbachem/php-ga)
- [semsol/arc2](https://github.com/semsol/arc2)
- [phalcon/invo](https://github.com/phalcon/invo)
- [robmorgan/phinx](https://github.com/robmorgan/phinx)
- [mpociot/botman](https://github.com/mpociot/botman)
- [youzan/zan](https://github.com/youzan/zan)
- [fguillot/picoFeed](https://github.com/fguillot/picoFeed)
- [sgolemon/table-flip](https://github.com/sgolemon/table-flip)
- [kloon/WooCommerce-REST-API-Client-Library](https://github.com/kloon/WooCommerce-REST-API-Client-Library)
- [doctrine/mongodb](https://github.com/doctrine/mongodb)
- [speedmax/h2o-php](https://github.com/speedmax/h2o-php)
- [consolibyte/quickbooks-php](https://github.com/consolibyte/quickbooks-php)
- [char0n/ffmpeg-php](https://github.com/char0n/ffmpeg-php)
- [tareq1988/wordpress-settings-api-class](https://github.com/tareq1988/wordpress-settings-api-class)
- [roadiz/roadiz](https://github.com/roadiz/roadiz)
- [phalcon/forum](https://github.com/phalcon/forum)
- [egulias/EmailValidator](https://github.com/egulias/EmailValidator)
- [danielmewes/php-rql](https://github.com/danielmewes/php-rql)
- [thephpleague/route](https://github.com/thephpleague/route)
- [phalcon/vokuro](https://github.com/phalcon/vokuro)
- [PHPFastCGI/FastCGIDaemon](https://github.com/PHPFastCGI/FastCGIDaemon)
- [MUlt1mate/cron-manager](https://github.com/MUlt1mate/cron-manager)
- [Indatus/trucker](https://github.com/Indatus/trucker)
- [Devristo/phpws](https://github.com/Devristo/phpws)
- [ihor/Nspl](https://github.com/ihor/Nspl)
- [danielstjules/pho](https://github.com/danielstjules/pho)
- [swoole/framework](https://github.com/swoole/framework)
- [padraic/humbug](https://github.com/padraic/humbug)
- [rilwis/meta-box](https://github.com/rilwis/meta-box)
- [elementary/website](https://github.com/elementary/website)
- [WellCommerce/WellCommerce](https://github.com/WellCommerce/WellCommerce)
- [ScriptFUSION/Porter](https://github.com/ScriptFUSION/Porter)
- [jimrubenstein/php-profiler](https://github.com/jimrubenstein/php-profiler)
- [imanee/imanee](https://github.com/imanee/imanee)
- [FriendsOfCake/CakePdf](https://github.com/FriendsOfCake/CakePdf)
- [thomasbachem/php-short-array-syntax-converter](https://github.com/thomasbachem/php-short-array-syntax-converter)
- [shumkov/Rediska](https://github.com/shumkov/Rediska)
- [padraic/mockery](https://github.com/padraic/mockery)
- [akalongman/php-telegram-bot](https://github.com/akalongman/php-telegram-bot)
- [ParsePlatform/parse-php-sdk](https://github.com/ParsePlatform/parse-php-sdk)
- [Porto-SAP/Hello-API](https://github.com/Porto-SAP/Hello-API)
- [sensiolabs/SensioGeneratorBundle](https://github.com/sensiolabs/SensioGeneratorBundle)
- [mandango/mandango](https://github.com/mandango/mandango)
- [Vectorface/dunit](https://github.com/Vectorface/dunit)
- [liip/LiipThemeBundle](https://github.com/liip/LiipThemeBundle)
- [dereuromark/cakephp-tools](https://github.com/dereuromark/cakephp-tools)
- [sillydong/CZD_Yaf_Extension](https://github.com/sillydong/CZD_Yaf_Extension)
- [pda/flexihash](https://github.com/pda/flexihash)
- [xPaw/PHP-Source-Query](https://github.com/xPaw/PHP-Source-Query)
- [InterNations/http-mock](https://github.com/InterNations/http-mock)
- [Herzult/php-ssh](https://github.com/Herzult/php-ssh)
- [Flynsarmy/PHPWebSocket-Chat](https://github.com/Flynsarmy/PHPWebSocket-Chat)
- [claviska/simple-php-captcha](https://github.com/claviska/simple-php-captcha)
- [xpressengine/xe-core](https://github.com/xpressengine/xe-core)
- [lexik/LexikFormFilterBundle](https://github.com/lexik/LexikFormFilterBundle)
- [avstudnitz/AvS_FastSimpleImport](https://github.com/avstudnitz/AvS_FastSimpleImport)
- [FriendsOfCake/crud](https://github.com/FriendsOfCake/crud)
- [raveren/kint](https://github.com/raveren/kint)
- [laravelio/laravel.io](https://github.com/laravelio/laravel.io)
- [humanmade/Colors-Of-Image](https://github.com/humanmade/Colors-Of-Image)
- [easychen/LazyPHP4](https://github.com/easychen/LazyPHP4)
- [wodby/docker4drupal](https://github.com/wodby/docker4drupal)
- [Mibew/mibew](https://github.com/Mibew/mibew)
- [Azure/azure-sdk-for-php](https://github.com/Azure/azure-sdk-for-php)
- [kriansa/openboleto](https://github.com/kriansa/openboleto)
- [doitlikejustin/amazon-wish-lister](https://github.com/doitlikejustin/amazon-wish-lister)
- [davesloan/mysql-php-migrations](https://github.com/davesloan/mysql-php-migrations)
- [theseer/Autoload](https://github.com/theseer/Autoload)
- [nrk/predis-async](https://github.com/nrk/predis-async)
- [tplaner/When](https://github.com/tplaner/When)
- [rase-/socket.io-php-emitter](https://github.com/rase-/socket.io-php-emitter)
- [jeremeamia/mu](https://github.com/jeremeamia/mu)
- [erusev/base](https://github.com/erusev/base)
- [Roave/StrictPhp](https://github.com/Roave/StrictPhp)
- [OWASP/rbac](https://github.com/OWASP/rbac)
- [troydavisson/PHRETS](https://github.com/troydavisson/PHRETS)
- [bugsnag/bugsnag-laravel](https://github.com/bugsnag/bugsnag-laravel)
- [alexbilbie/Proton](https://github.com/alexbilbie/Proton)
- [phanbook/phanbook](https://github.com/phanbook/phanbook)
- [chregu/GoogleAuthenticator.php](https://github.com/chregu/GoogleAuthenticator.php)
- [mytharcher/alipay-php-sdk](https://github.com/mytharcher/alipay-php-sdk)
- [gjedeer/celery-php](https://github.com/gjedeer/celery-php)
- [kevinlebrun/colors.php](https://github.com/kevinlebrun/colors.php)
- [isaacsu/twich](https://github.com/isaacsu/twich)
- [ludovicchabant/PieCrust](https://github.com/ludovicchabant/PieCrust)
- [jasonlewis/expressive-date](https://github.com/jasonlewis/expressive-date)
- [startbbs/startbbs](https://github.com/startbbs/startbbs)
- [AlloVince/EvaOAuth](https://github.com/AlloVince/EvaOAuth)
- [madcoda/php-youtube-api](https://github.com/madcoda/php-youtube-api)
- [ddeboer/imap](https://github.com/ddeboer/imap)
- [salsify/jsonstreamingparser](https://github.com/salsify/jsonstreamingparser)
- [mptre/php-soundcloud](https://github.com/mptre/php-soundcloud)
- [FluentDOM/FluentDOM](https://github.com/FluentDOM/FluentDOM)
- [BaunCMS/Baun](https://github.com/BaunCMS/Baun)
- [twip/twip](https://github.com/twip/twip)
- [Gargron/fileupload](https://github.com/Gargron/fileupload)
- [dready92/PHP-on-Couch](https://github.com/dready92/PHP-on-Couch)
- [stojg/crop](https://github.com/stojg/crop)
- [schmittjoh/php-collection](https://github.com/schmittjoh/php-collection)
- [liip/php-osx](https://github.com/liip/php-osx)
- [dddinphp/last-wishes](https://github.com/dddinphp/last-wishes)
- [calvinfroedge/codeigniter-payments](https://github.com/calvinfroedge/codeigniter-payments)
- [Exeu/Amazon-ECS-PHP-Library](https://github.com/Exeu/Amazon-ECS-PHP-Library)
- [naneau/php-obfuscator](https://github.com/naneau/php-obfuscator)
- [jbroadway/analog](https://github.com/jbroadway/analog)
- [evernote/evernote-sdk-php](https://github.com/evernote/evernote-sdk-php)
- [mikehaertl/php-pdftk](https://github.com/mikehaertl/php-pdftk)
- [skyronic/crudkit](https://github.com/skyronic/crudkit)
- [jamesgpearce/modernizr-server](https://github.com/jamesgpearce/modernizr-server)
- [facebook/facebook-php-ads-sdk](https://github.com/facebook/facebook-php-ads-sdk)
- [Athari/YaLinqo](https://github.com/Athari/YaLinqo)
- [shrikeh/teapot](https://github.com/shrikeh/teapot)
- [machuga/authority](https://github.com/machuga/authority)
- [LExpress/symfony1](https://github.com/LExpress/symfony1)
- [joetannenbaum/mr-clean](https://github.com/joetannenbaum/mr-clean)
- [braintree/braintree_php](https://github.com/braintree/braintree_php)
- [X2Engine/X2CRM](https://github.com/X2Engine/X2CRM)
- [jkoudys/immutable.php](https://github.com/jkoudys/immutable.php)
- [seatgeek/djjob](https://github.com/seatgeek/djjob)
- [xiaosier/libweibo](https://github.com/xiaosier/libweibo)
- [markwilson/VerbalExpressionsPhp](https://github.com/markwilson/VerbalExpressionsPhp)
- [browscap/browscap-php](https://github.com/browscap/browscap-php)
- [njh/easyrdf](https://github.com/njh/easyrdf)
- [mamuz/PhpDependencyAnalysis](https://github.com/mamuz/PhpDependencyAnalysis)
- [Stolz/Assets](https://github.com/Stolz/Assets)
- [runekaagaard/snowscript](https://github.com/runekaagaard/snowscript)
- [Inchoo/Inchoo_PHP7](https://github.com/Inchoo/Inchoo_PHP7)
- [michael-romer/zf-boilerplate](https://github.com/michael-romer/zf-boilerplate)
- [jwage/easy-csv](https://github.com/jwage/easy-csv)
- [jmespath/jmespath.php](https://github.com/jmespath/jmespath.php)
- [donatj/PhpUserAgent](https://github.com/donatj/PhpUserAgent)
- [alxlit/coffeescript-php](https://github.com/alxlit/coffeescript-php)
- [wanze/Google-Analytics-API-PHP](https://github.com/wanze/Google-Analytics-API-PHP)
- [punkave/phpQuery](https://github.com/punkave/phpQuery)
- [jakubkulhan/bunny](https://github.com/jakubkulhan/bunny)
- [ircmaxell/PhpGenerics](https://github.com/ircmaxell/PhpGenerics)
- [elfet/console](https://github.com/elfet/console)
- [digitalnature/php-ref](https://github.com/digitalnature/php-ref)
- [whatthejeff/nyancat-phpunit-resultprinter](https://github.com/whatthejeff/nyancat-phpunit-resultprinter)
- [koconder/android-market-api-php](https://github.com/koconder/android-market-api-php)
- [johnkary/phpunit-speedtrap](https://github.com/johnkary/phpunit-speedtrap)
- [gilbitron/PIP](https://github.com/gilbitron/PIP)
- [apache/incubator-predictionio-sdk-php](https://github.com/apache/incubator-predictionio-sdk-php)
- [Seldaek/jsonlint](https://github.com/Seldaek/jsonlint)
- [Lakion/Lionframe](https://github.com/Lakion/Lionframe)
- [inoerp/inoERP](https://github.com/inoerp/inoERP)
- [gburtini/Learning-Library-for-PHP](https://github.com/gburtini/Learning-Library-for-PHP)
- [teqneers/PHP-Stream-Wrapper-for-Git](https://github.com/teqneers/PHP-Stream-Wrapper-for-Git)
- [symfony/polyfill](https://github.com/symfony/polyfill)
- [Kroc/NoNonsenseForum](https://github.com/Kroc/NoNonsenseForum)
- [eschnou/storytlr](https://github.com/eschnou/storytlr)
- [colinmollenhour/mongodb-php-odm](https://github.com/colinmollenhour/mongodb-php-odm)
- [igorw/ConfigServiceProvider](https://github.com/igorw/ConfigServiceProvider)
- [SocalNick/ScnSocialAuth](https://github.com/SocalNick/ScnSocialAuth)
- [peridot-php/peridot](https://github.com/peridot-php/peridot)
- [padawan-php/padawan.php](https://github.com/padawan-php/padawan.php)
- [hightman/pspider](https://github.com/hightman/pspider)
- [bandwidth-throttle/token-bucket](https://github.com/bandwidth-throttle/token-bucket)
- [mikeemoo/ColorJizz-PHP](https://github.com/mikeemoo/ColorJizz-PHP)
- [jamesmoss/flywheel](https://github.com/jamesmoss/flywheel)
- [elidickinson/php-export-data](https://github.com/elidickinson/php-export-data)
- [tj/php-selector](https://github.com/tj/php-selector)
- [jsebrech/php-o](https://github.com/jsebrech/php-o)
- [cosenary/Simple-PHP-Cache](https://github.com/cosenary/Simple-PHP-Cache)
- [PiPHP/GPIO](https://github.com/PiPHP/GPIO)
- [nmred/kafka-php](https://github.com/nmred/kafka-php)
- [phpsec/phpSec](https://github.com/phpsec/phpSec)
- [panique/php-long-polling](https://github.com/panique/php-long-polling)
- [whatthejeff/breeze](https://github.com/whatthejeff/breeze)
- [raulfraile/distill](https://github.com/raulfraile/distill)
- [mathiasbynens/php-url-shortener](https://github.com/mathiasbynens/php-url-shortener)
- [kohkimakimoto/altax](https://github.com/kohkimakimoto/altax)
- [jwilsson/spotify-web-api-php](https://github.com/jwilsson/spotify-web-api-php)
- [johnlui/AliyunOSS](https://github.com/johnlui/AliyunOSS)
- [SmItH197/SteamAuthentication](https://github.com/SmItH197/SteamAuthentication)
- [Level-2/Transphporm](https://github.com/Level-2/Transphporm)
- [JorgenPhi/php-snapchat](https://github.com/JorgenPhi/php-snapchat)
- [klokantech/tileserver-php](https://github.com/klokantech/tileserver-php)
- [jwage/phpchunkit](https://github.com/jwage/phpchunkit)
- [ClassPreloader/ClassPreloader](https://github.com/ClassPreloader/ClassPreloader)
- [tlack/snaphax](https://github.com/tlack/snaphax)
- [stil/curl-easy](https://github.com/stil/curl-easy)
- [lastguest/mu](https://github.com/lastguest/mu)
- [domnikl/statsd-php](https://github.com/domnikl/statsd-php)
- [BitOne/php-meminfo](https://github.com/BitOne/php-meminfo)
- [asm89/Rx.PHP](https://github.com/asm89/Rx.PHP)
- [Sybio/GifCreator](https://github.com/Sybio/GifCreator)
- [php-amqplib/Thumper](https://github.com/php-amqplib/Thumper)
- [flack/createphp](https://github.com/flack/createphp)
- [cpliakas/git-wrapper](https://github.com/cpliakas/git-wrapper)
- [campaignmonitor/createsend-php](https://github.com/campaignmonitor/createsend-php)
- [regru/php-whois](https://github.com/regru/php-whois)
- [egeloen/ivory-google-map](https://github.com/egeloen/ivory-google-map)
- [prooph/service-bus](https://github.com/prooph/service-bus)
- [magento-ecg/coding-standard](https://github.com/magento-ecg/coding-standard)
- [GeekZooStudio/ECMobile_PHP](https://github.com/GeekZooStudio/ECMobile_PHP)
- [caoym/phprs-restful](https://github.com/caoym/phprs-restful)
- [andre487/php_rutils](https://github.com/andre487/php_rutils)
- [AuthorizeNet/sdk-php](https://github.com/AuthorizeNet/sdk-php)
- [rchouinard/phpass](https://github.com/rchouinard/phpass)
- [etsy/phpunit-extensions](https://github.com/etsy/phpunit-extensions)
- [bootsz/wp-advanced-search](https://github.com/bootsz/wp-advanced-search)
- [Adldap2/Adldap2](https://github.com/Adldap2/Adldap2)
- [jonathantorres/construct](https://github.com/jonathantorres/construct)
- [e107inc/e107](https://github.com/e107inc/e107)
- [widmogrod/php-functional](https://github.com/widmogrod/php-functional)
- [mtdowling/transducers.php](https://github.com/mtdowling/transducers.php)
- [hfcorriez/pagon](https://github.com/hfcorriez/pagon)
- [fzaninotto/Streamer](https://github.com/fzaninotto/Streamer)
- [chrisboulton/php-resque-scheduler](https://github.com/chrisboulton/php-resque-scheduler)
- [commerceguys/intl](https://github.com/commerceguys/intl)
- [alchemy-fr/Zippy](https://github.com/alchemy-fr/Zippy)
- [shameerc/TextPress](https://github.com/shameerc/TextPress)
- [dropbox/dropbox-sdk-php](https://github.com/dropbox/dropbox-sdk-php)
- [tamagokun/pomander](https://github.com/tamagokun/pomander)
- [mishamx/yii-user](https://github.com/mishamx/yii-user)
- [gilbitron/PHP-SimpleCache](https://github.com/gilbitron/PHP-SimpleCache)
- [badoo/soft-mocks](https://github.com/badoo/soft-mocks)
- [php-school/learn-you-php](https://github.com/php-school/learn-you-php)
- [nicmart/Tree](https://github.com/nicmart/Tree)
- [modolabs/Kurogo-Mobile-Web](https://github.com/modolabs/Kurogo-Mobile-Web)
- [fieryprophet/php-sandbox](https://github.com/fieryprophet/php-sandbox)
- [Austinb/GameQ](https://github.com/Austinb/GameQ)
- [reactphp/socket](https://github.com/reactphp/socket)
- [opensource-socialnetwork/opensource-socialnetwork](https://github.com/opensource-socialnetwork/opensource-socialnetwork)
- [fire015/flintstone](https://github.com/fire015/flintstone)
- [TelegramBot/Api](https://github.com/TelegramBot/Api)
- [davidscotttufts/php-barcode](https://github.com/davidscotttufts/php-barcode)
- [brannondorsey/apibuilder](https://github.com/brannondorsey/apibuilder)
- [bramus/router](https://github.com/bramus/router)
- [phly/conduit](https://github.com/phly/conduit)
- [Bacon/BaconQrCode](https://github.com/Bacon/BaconQrCode)
- [andersondanilo/CnabPHP](https://github.com/andersondanilo/CnabPHP)
- [vimeo/vimeo-php-lib](https://github.com/vimeo/vimeo-php-lib)
- [jstayton/Miner](https://github.com/jstayton/Miner)
- [ivkos/Pushbullet-for-PHP](https://github.com/ivkos/Pushbullet-for-PHP)
- [Hood3dRob1n/SQLMAP-Web-GUI](https://github.com/Hood3dRob1n/SQLMAP-Web-GUI)
- [sesser/Instaphp](https://github.com/sesser/Instaphp)
- [jpush/jpush-api-php-client](https://github.com/jpush/jpush-api-php-client)
- [filamentgroup/quickconcat](https://github.com/filamentgroup/quickconcat)
- [cheshirecats/CuriousWall](https://github.com/cheshirecats/CuriousWall)
- [alexbilbie/MongoQB](https://github.com/alexbilbie/MongoQB)
- [vladkens/VK](https://github.com/vladkens/VK)
- [gitonomy/gitlib](https://github.com/gitonomy/gitlib)
- [getjump/VkApiPHP](https://github.com/getjump/VkApiPHP)
- [Nicolab/php-ftp-client](https://github.com/Nicolab/php-ftp-client)
- [marcioAlmada/annotations](https://github.com/marcioAlmada/annotations)
- [marcelog/PAMI](https://github.com/marcelog/PAMI)
- [mac-cain13/notificato](https://github.com/mac-cain13/notificato)
- [JWHennessey/phpInsight](https://github.com/JWHennessey/phpInsight)
- [backbee/backbee-php](https://github.com/backbee/backbee-php)
- [alexgarrett/violin](https://github.com/alexgarrett/violin)
- [vespolina/vespolina-sandbox](https://github.com/vespolina/vespolina-sandbox)
- [rustem-art/hd.rustem](https://github.com/rustem-art/hd.rustem)
- [pinceladasdaweb/Simple-PHP-Contact-Form](https://github.com/pinceladasdaweb/Simple-PHP-Contact-Form)
- [webasyst/webasyst-framework](https://github.com/webasyst/webasyst-framework)
- [o/sitemap-php](https://github.com/o/sitemap-php)
- [fmalk/codeigniter-phpunit](https://github.com/fmalk/codeigniter-phpunit)
- [fkooman/php-oauth-as](https://github.com/fkooman/php-oauth-as)
- [ircmaxell/monad-php](https://github.com/ircmaxell/monad-php)
- [huyanping/php_crontab](https://github.com/huyanping/php_crontab)
- [atlasphp/Atlas.Orm](https://github.com/atlasphp/Atlas.Orm)
- [indeyets/pake](https://github.com/indeyets/pake)
- [dan-coulter/phpflickr](https://github.com/dan-coulter/phpflickr)
- [Scriptor/pharen](https://github.com/Scriptor/pharen)
- [goglezon/OSAdmin](https://github.com/goglezon/OSAdmin)
- [chibimagic/WebDriver-PHP](https://github.com/chibimagic/WebDriver-PHP)
- [ADOdb/ADOdb](https://github.com/ADOdb/ADOdb)
- [jwage/php-mongodb-admin](https://github.com/jwage/php-mongodb-admin)
- [jmstriegel/php.googleplusapi](https://github.com/jmstriegel/php.googleplusapi)
- [coduo/php-matcher](https://github.com/coduo/php-matcher)
- [Andrewsville/PHP-Token-Reflection](https://github.com/Andrewsville/PHP-Token-Reflection)
- [webmozart/console](https://github.com/webmozart/console)
- [vimeo/vimeo.php](https://github.com/vimeo/vimeo.php)
- [marmelab/microrest.php](https://github.com/marmelab/microrest.php)
- [macuenca/Instagram-PHP-API](https://github.com/macuenca/Instagram-PHP-API)
- [guzzle/RingPHP](https://github.com/guzzle/RingPHP)
- [feulf/raintpl](https://github.com/feulf/raintpl)
- [ceesvanegmond/minify](https://github.com/ceesvanegmond/minify)
- [bluerhinos/phpMQTT](https://github.com/bluerhinos/phpMQTT)
- [bainternet/PHP-Hooks](https://github.com/bainternet/PHP-Hooks)
- [LeaVerou/rgba.php](https://github.com/LeaVerou/rgba.php)
- [kelunik/acme-client](https://github.com/kelunik/acme-client)
- [kapolos/pramda](https://github.com/kapolos/pramda)
- [angelleye/paypal-php-library](https://github.com/angelleye/paypal-php-library)
- [ua-parser/uap-php](https://github.com/ua-parser/uap-php)
- [antirez/retwis](https://github.com/antirez/retwis)
- [CpanelInc/xmlapi-php](https://github.com/CpanelInc/xmlapi-php)
- [indieteq/indieteq-php-my-sql-pdo-database-class](https://github.com/indieteq/indieteq-php-my-sql-pdo-database-class)
- [corneltek/LazyRecord](https://github.com/corneltek/LazyRecord)
- [Xowap/PHP-Serial](https://github.com/Xowap/PHP-Serial)
- [webmozart/expression](https://github.com/webmozart/expression)
- [Surzhikov/TelegramSiteHelper](https://github.com/Surzhikov/TelegramSiteHelper)
- [phergie/phergie](https://github.com/phergie/phergie)
- [loic-sharma/profiler](https://github.com/loic-sharma/profiler)
- [odesk/phystrix](https://github.com/odesk/phystrix)
- [blackfireio/player](https://github.com/blackfireio/player)
- [mkusher/padawan.php](https://github.com/mkusher/padawan.php)
- [tutumcloud/apache-php](https://github.com/tutumcloud/apache-php)
- [ligboy/Wechat-php](https://github.com/ligboy/Wechat-php)
- [toin0u/Geotools-laravel](https://github.com/toin0u/Geotools-laravel)
- [suin/php-rss-writer](https://github.com/suin/php-rss-writer)
- [phpspec/phpspec2-proof-of-concept](https://github.com/phpspec/phpspec2-proof-of-concept)
- [lkorth/php-gcm](https://github.com/lkorth/php-gcm)
- [KnpLabs/KnpMarkdownBundle](https://github.com/KnpLabs/KnpMarkdownBundle)
- [JetBrains/phpstorm-workshop](https://github.com/JetBrains/phpstorm-workshop)
- [JamesHeinrich/phpThumb](https://github.com/JamesHeinrich/phpThumb)
- [blongden/hal](https://github.com/blongden/hal)
- [zendframework/zend-expressive](https://github.com/zendframework/zend-expressive)
- [mpociot/slackbot](https://github.com/mpociot/slackbot)
- [php-integrator/atom-base](https://github.com/php-integrator/atom-base)
- [scil/LaravelFly](https://github.com/scil/LaravelFly)
- [f/kapi](https://github.com/f/kapi)
- [kellan/pinterest.api.php](https://github.com/kellan/pinterest.api.php)
- [flourishlib/flourish-old](https://github.com/flourishlib/flourish-old)
- [sphido/cms](https://github.com/sphido/cms)
- [jim/fitzgerald](https://github.com/jim/fitzgerald)
- [jimdoescode/CodeIgniter-Dropbox-API-Library](https://github.com/jimdoescode/CodeIgniter-Dropbox-API-Library)
- [hipchat/hipchat-php](https://github.com/hipchat/hipchat-php)
- [eyecatchup/php-yt_downloader](https://github.com/eyecatchup/php-yt_downloader)
- [dg/ftp-php](https://github.com/dg/ftp-php)
- [Mahmoudz/Hello-API](https://github.com/Mahmoudz/Hello-API)
- [jdp/twitterlibphp](https://github.com/jdp/twitterlibphp)
- [DevGrow/jQuery-Mobile-PHP-MVC](https://github.com/DevGrow/jQuery-Mobile-PHP-MVC)
- [vladgh/VladGh.com-LEMP](https://github.com/vladgh/VladGh.com-LEMP)
- [phpmo/php.mo](https://github.com/phpmo/php.mo)
- [ornicar/php-git-repo](https://github.com/ornicar/php-git-repo)
- [Nakiami/mellivora](https://github.com/Nakiami/mellivora)
- [jakubledl/dissect](https://github.com/jakubledl/dissect)
- [afreiday/php-waveform-png](https://github.com/afreiday/php-waveform-png)
- [jgrossi/corcel](https://github.com/jgrossi/corcel)
- [ssddanbrown/BookStack](https://github.com/ssddanbrown/BookStack)
- [JorgenPhid/php-snapchat](https://github.com/JorgenPhid/php-snapchat)
- [drewm/morse](https://github.com/drewm/morse)
- [laravelbook/laravel4-phpstorm-helper](https://github.com/laravelbook/laravel4-phpstorm-helper)
- [jayli/combo](https://github.com/jayli/combo)
- [dflydev/dflydev-markdown](https://github.com/dflydev/dflydev-markdown)
- [reisraff/phulp](https://github.com/reisraff/phulp)
- [kamranahmedse/php-geocode](https://github.com/kamranahmedse/php-geocode)
- [dryphp/bitcoin.php](https://github.com/dryphp/bitcoin.php)
- [analogic/lescript](https://github.com/analogic/lescript)
- [consolidation-org/Robo](https://github.com/consolidation-org/Robo)
- [ryancramerdesign/ProcessWire](https://github.com/ryancramerdesign/ProcessWire)
- [crysalead/kahlan](https://github.com/crysalead/kahlan)
- [facebook/facebook-php-sdk-v4](https://github.com/facebook/facebook-php-sdk-v4)
- [claudehohl/Stikked](https://github.com/claudehohl/Stikked)
- [briancray/PHP-URL-Shortener](https://github.com/briancray/PHP-URL-Shortener)
- [storytlr/storytlr](https://github.com/storytlr/storytlr)
- [PredictionIO/PredictionIO-PHP-SDK](https://github.com/PredictionIO/PredictionIO-PHP-SDK)
- [eddiejaoude/Zend-Framework--Doctrine-ORM--PHPUnit--Ant--Jenkins-CI--TDD-](https://github.com/eddiejaoude/Zend-Framework--Doctrine-ORM--PHPUnit--Ant--Jenkins-CI--TDD-)
- [Xeoncross/forumfive](https://github.com/Xeoncross/forumfive)
- [andrewvy/HHVMCraft](https://github.com/andrewvy/HHVMCraft)
- [josegonzalez/php-git](https://github.com/josegonzalez/php-git)
- [firephp/firephp-core](https://github.com/firephp/firephp-core)
- [samayo/bulletproof](https://github.com/samayo/bulletproof)
- [mikegogulski/bitcoin-php](https://github.com/mikegogulski/bitcoin-php)
- [chrissimpkins/tweetledee](https://github.com/chrissimpkins/tweetledee)
- [calinrada/php-apidoc](https://github.com/calinrada/php-apidoc)
- [MongoDB-Rox/phpMoAdmin-MongoDB-Admin-Tool-for-PHP](https://github.com/MongoDB-Rox/phpMoAdmin-MongoDB-Admin-Tool-for-PHP)
- [cweiske/phorkie](https://github.com/cweiske/phorkie)
- [mako-framework/framework](https://github.com/mako-framework/framework)
- [aaronpk/Google-Voice-PHP-API](https://github.com/aaronpk/Google-Voice-PHP-API)
- [psecio/versionscan](https://github.com/psecio/versionscan)
- [feulf/raintpl3](https://github.com/feulf/raintpl3)
- [buttercup-php/protects](https://github.com/buttercup-php/protects)
- [briancray/phpA-B](https://github.com/briancray/phpA-B)
- [Grandt/PHPePub](https://github.com/Grandt/PHPePub)
- [Dropbox-PHP/dropbox-php](https://github.com/Dropbox-PHP/dropbox-php)
- [atk4/atk4](https://github.com/atk4/atk4)
- [textile/php-textile](https://github.com/textile/php-textile)
- [koraktor/steam-condenser-php](https://github.com/koraktor/steam-condenser-php)
- [Codegyre/Robo](https://github.com/Codegyre/Robo)
- [snipe/snipe-it](https://github.com/snipe/snipe-it)
- [fpdo/fluentpdo](https://github.com/fpdo/fluentpdo)
- [scrutinizer-ci/php-analyzer](https://github.com/scrutinizer-ci/php-analyzer)
- [CodeScaleInc/ffmpeg-php](https://github.com/CodeScaleInc/ffmpeg-php)
- [rainphp/raintpl](https://github.com/rainphp/raintpl)
- [rainphp/raintpl3](https://github.com/rainphp/raintpl3)
- [CodeMeme/Phingistrano](https://github.com/CodeMeme/Phingistrano)
- [chanmix51/Pomm](https://github.com/chanmix51/Pomm)
- [nette/tester](https://github.com/nette/tester)
- [Znarkus/postmark-php](https://github.com/Znarkus/postmark-php)
- [sbisbee/sag](https://github.com/sbisbee/sag)
- [mattg888/GCM-PHP-Server-Push-Message](https://github.com/mattg888/GCM-PHP-Server-Push-Message)
- [hownowstephen/php-foursquare](https://github.com/hownowstephen/php-foursquare)
- [basho/riak-php-client](https://github.com/basho/riak-php-client)
- [adamgriffiths/ag-auth](https://github.com/adamgriffiths/ag-auth)
- [toin0u/DigitalOcean](https://github.com/toin0u/DigitalOcean)
- [kzykhys/PHPGit](https://github.com/kzykhys/PHPGit)
- [jeremeamia/acclimate-container](https://github.com/jeremeamia/acclimate-container)
- [dignajar/nibbleblog](https://github.com/dignajar/nibbleblog)
- [RickySu/phpsocket.io](https://github.com/RickySu/phpsocket.io)
- [rsms/gitblog](https://github.com/rsms/gitblog)
- [lphuberdeau/Neo4j-PHP-OGM](https://github.com/lphuberdeau/Neo4j-PHP-OGM)
- [facebook/FBMock](https://github.com/facebook/FBMock)
- [jbroadway/elefant](https://github.com/jbroadway/elefant)
- [glamorous/TMDb-PHP-API](https://github.com/glamorous/TMDb-PHP-API)
- [e-oz/Memory](https://github.com/e-oz/Memory)
- [buggedcom/phpvideotoolkit-v2](https://github.com/buggedcom/phpvideotoolkit-v2)
- [Arara/Process](https://github.com/Arara/Process)
- [munkireport/munkireport-php](https://github.com/munkireport/munkireport-php)
- [ircmaxell/PHP-CryptLib](https://github.com/ircmaxell/PHP-CryptLib)
- [phpbrew/phpbrew](https://github.com/phpbrew/phpbrew)
- [chriso/klein.php](https://github.com/chriso/klein.php)
- [liu21st/thinkphp](https://github.com/liu21st/thinkphp)
- [WHAnonymous/Chat-API](https://github.com/WHAnonymous/Chat-API)
- [videlalvaro/php-amqplib](https://github.com/videlalvaro/php-amqplib)
- [khoaofgod/phpfastcache](https://github.com/khoaofgod/phpfastcache)
- [mathiasverraes/money](https://github.com/mathiasverraes/money)
- [rlerdorf/phan](https://github.com/rlerdorf/phan)
- [lichtner/fluentpdo](https://github.com/lichtner/fluentpdo)
- [johmue/mysql-workbench-schema-exporter](https://github.com/johmue/mysql-workbench-schema-exporter)
- [badphp/dispatch](https://github.com/badphp/dispatch)
- [getsentry/raven-php](https://github.com/getsentry/raven-php)
- [netresearch/jsonmapper](https://github.com/netresearch/jsonmapper)
- [indieteq/PHP-MySQL-PDO-Database-Class](https://github.com/indieteq/PHP-MySQL-PDO-Database-Class)
- [bastianallgeier/kirby](https://github.com/bastianallgeier/kirby)
- [nonsalant/contract](https://github.com/nonsalant/contract)
- [erusev/parsedown-extra](https://github.com/erusev/parsedown-extra)
- [stage1/docker-php](https://github.com/stage1/docker-php)
- [phundament/app](https://github.com/phundament/app)
- [OWASP/phpsec](https://github.com/OWASP/phpsec)
- [codeliner/php-ddd-cargo-sample](https://github.com/codeliner/php-ddd-cargo-sample)
- [videlalvaro/Thumper](https://github.com/videlalvaro/Thumper)
- [ivanproskuryakov/Aisel](https://github.com/ivanproskuryakov/Aisel)
- [TurbineCSS/Turbine](https://github.com/TurbineCSS/Turbine)
- [lisphp/lisphp](https://github.com/lisphp/lisphp)
- [bobthecow/Faker](https://github.com/bobthecow/Faker)
- [sdboyer/gliph](https://github.com/sdboyer/gliph)
- [charliesome/Fructose](https://github.com/charliesome/Fructose)
- [tschoffelen/PHP-Passkit](https://github.com/tschoffelen/PHP-Passkit)
- [chriskite/phactory](https://github.com/chriskite/phactory)
- [barbushin/dater](https://github.com/barbushin/dater)
- [doctrine/phpcr-odm](https://github.com/doctrine/phpcr-odm)
- [doctrine/orientdb-odm](https://github.com/doctrine/orientdb-odm)
- [bitcoin-blockexplorer/old-blockexplorer-php](https://github.com/bitcoin-blockexplorer/old-blockexplorer-php)
- [mattstauffer/Simple-RESS](https://github.com/mattstauffer/Simple-RESS)
- [lstrojny/phpunit-clever-and-smart](https://github.com/lstrojny/phpunit-clever-and-smart)
- [crodas/Haanga](https://github.com/crodas/Haanga)
- [tylerhall/php-growl](https://github.com/tylerhall/php-growl)
- [efficiently/authority-controller](https://github.com/efficiently/authority-controller)
- [hassankhan/Syngr](https://github.com/hassankhan/Syngr)
- [calvinfroedge/PHP-Payments](https://github.com/calvinfroedge/PHP-Payments)
- [pagekit/razr](https://github.com/pagekit/razr)
- [ornicar/php-user-agent](https://github.com/ornicar/php-user-agent)
- [kvz/system_daemon](https://github.com/kvz/system_daemon)
- [fkooman/php-oauth-client](https://github.com/fkooman/php-oauth-client)
- [Falicon/BitlyPHP](https://github.com/Falicon/BitlyPHP)
- [webtechnick/CakePHP-FileUpload-Plugin](https://github.com/webtechnick/CakePHP-FileUpload-Plugin)
- [sebastianbergmann/phpunit-mock-objects](https://github.com/sebastianbergmann/phpunit-mock-objects)
- [osalabs/phpminiadmin](https://github.com/osalabs/phpminiadmin)
- [mattab/trello-backup](https://github.com/mattab/trello-backup)
- [debuggable/php_arrays](https://github.com/debuggable/php_arrays)
- [akDeveloper/Aktive-Merchant](https://github.com/akDeveloper/Aktive-Merchant)
- [jtopjian/gluephp](https://github.com/jtopjian/gluephp)
- [jdp/redisent](https://github.com/jdp/redisent)
- [bergie/phpflo](https://github.com/bergie/phpflo)
- [tnc/php-amqplib](https://github.com/tnc/php-amqplib)
- [whizark/php-patterns](https://github.com/whizark/php-patterns)
- [olamedia/nokogiri](https://github.com/olamedia/nokogiri)
- [hafriedlander/php-peg](https://github.com/hafriedlander/php-peg)
- [sebastianbergmann/dbunit](https://github.com/sebastianbergmann/dbunit)
- [akanehara/ginq](https://github.com/akanehara/ginq)
- [stripe/wilde-things](https://github.com/stripe/wilde-things)
- [phly/phly_mustache](https://github.com/phly/phly_mustache)
- [paypal/merchant-sdk-php](https://github.com/paypal/merchant-sdk-php)
- [marco-fiset/Testify.php](https://github.com/marco-fiset/Testify.php)
- [keyvanakbary/medusa](https://github.com/keyvanakbary/medusa)
- [funkatron/inspekt](https://github.com/funkatron/inspekt)
- [fluent/fluent-logger-php](https://github.com/fluent/fluent-logger-php)
- [dbtlr/php-airbrake](https://github.com/dbtlr/php-airbrake)
- [Mparaiso/Silex-Blog-App](https://github.com/Mparaiso/Silex-Blog-App)
- [davideme/libphonenumber-for-PHP](https://github.com/davideme/libphonenumber-for-PHP)
- [dzuelke/HadooPHP](https://github.com/dzuelke/HadooPHP)
- [thenbrent/paypal-digital-goods](https://github.com/thenbrent/paypal-digital-goods)
- [psynaptic/php-drupal.tmbundle](https://github.com/psynaptic/php-drupal.tmbundle)
- [jeteokeeffe/php-hmac-rest-api](https://github.com/jeteokeeffe/php-hmac-rest-api)
- [digitalbazaar/php-json-ld](https://github.com/digitalbazaar/php-json-ld)
- [andrewbiggart/latest-tweets-php-o-auth](https://github.com/andrewbiggart/latest-tweets-php-o-auth)
- [textmate/php.tmbundle](https://github.com/textmate/php.tmbundle)
- [ianckc/CodeIgniter-Instagram-Library](https://github.com/ianckc/CodeIgniter-Instagram-Library)
- [biangbiang/wxpay-php](https://github.com/biangbiang/wxpay-php)
- [alecsammon/php-raml-parser](https://github.com/alecsammon/php-raml-parser)
- [jbroadway/phpactiveresource](https://github.com/jbroadway/phpactiveresource)
- [googleglass/mirror-quickstart-php](https://github.com/googleglass/mirror-quickstart-php)
- [ezimuel/PHP-design-patterns](https://github.com/ezimuel/PHP-design-patterns)
- [antonioribeiro/laravelcs](https://github.com/antonioribeiro/laravelcs)
- [andraskende/cakephp-shopping-cart](https://github.com/andraskende/cakephp-shopping-cart)
- [jolicode/php-ar-drone](https://github.com/jolicode/php-ar-drone)
- [booruguru/UserPie](https://github.com/booruguru/UserPie)
- [achingbrain/php5-akismet](https://github.com/achingbrain/php5-akismet)
- [Andre-487/php_rutils](https://github.com/Andre-487/php_rutils)
- [geekcompany/LazyPHP4](https://github.com/geekcompany/LazyPHP4)
- [FokkeZB/TiCons-Server-PHP](https://github.com/FokkeZB/TiCons-Server-PHP)
- [MatthewRuddy/Wordpress-Timthumb-alternative](https://github.com/MatthewRuddy/Wordpress-Timthumb-alternative)
- [dwisetiyadi/CodeIgniter-PHP-QR-Code](https://github.com/dwisetiyadi/CodeIgniter-PHP-QR-Code)
- [vlucas/phpDataMapper](https://github.com/vlucas/phpDataMapper)
- [taskphp/task](https://github.com/taskphp/task)
- [oscarotero/imagecow](https://github.com/oscarotero/imagecow)
- [etsy/TryLib](https://github.com/etsy/TryLib)
- [fujimoto/php-skype](https://github.com/fujimoto/php-skype)
- [chobie/php-sundown](https://github.com/chobie/php-sundown)
- [authy/authy-php](https://github.com/authy/authy-php)
- [phacility/libphutil](https://github.com/phacility/libphutil)
- [Halleck45/PhpMetrics](https://github.com/Halleck45/PhpMetrics)
- [PHPOffice/PHPPowerPoint](https://github.com/PHPOffice/PHPPowerPoint)
- [kasperisager/phpstack](https://github.com/kasperisager/phpstack)
- [TomBZombie/Dice](https://github.com/TomBZombie/Dice)
- [gabrielbull/php-browser](https://github.com/gabrielbull/php-browser)
- [panique/php-login-one-file](https://github.com/panique/php-login-one-file)
- [wes/phpimageresize](https://github.com/wes/phpimageresize)
- [bortuzar/PHP-Mysql---Apple-Push-Notification-Server](https://github.com/bortuzar/PHP-Mysql---Apple-Push-Notification-Server)
- [lunaru/MongoRecord](https://github.com/lunaru/MongoRecord)
- [tlhunter/spidermonkey](https://github.com/tlhunter/spidermonkey)
- [evantahler/PHP-DAVE-API](https://github.com/evantahler/PHP-DAVE-API)
- [eryx/php-framework-benchmark](https://github.com/eryx/php-framework-benchmark)
- [yandod/php5-nginx-vagrant-sample](https://github.com/yandod/php5-nginx-vagrant-sample)
- [oyejorge/gpEasy-CMS](https://github.com/oyejorge/gpEasy-CMS)
- [kallaspriit/Cassandra-PHP-Client-Library](https://github.com/kallaspriit/Cassandra-PHP-Client-Library)
- [jeremykendall/password-validator](https://github.com/jeremykendall/password-validator)
- [disqus/disqus-php](https://github.com/disqus/disqus-php)
- [mikecao/sparrow](https://github.com/mikecao/sparrow)
- [pheryjs/phery](https://github.com/pheryjs/phery)
- [mybuilder/cronos](https://github.com/mybuilder/cronos)
- [harrydeluxe/php-liquid](https://github.com/harrydeluxe/php-liquid)
- [WebTales/rubedo](https://github.com/WebTales/rubedo)
- [mtibben/html2text](https://github.com/mtibben/html2text)
- [gpbmike/PHP-YUI-Compressor](https://github.com/gpbmike/PHP-YUI-Compressor)
- [drewjoh/phpPayPal](https://github.com/drewjoh/phpPayPal)
- [podio/podio-php](https://github.com/podio/podio-php)
- [jasonlewis/resource-watcher](https://github.com/jasonlewis/resource-watcher)
- [arshaw/phpti](https://github.com/arshaw/phpti)
- [silverstripe/silverstripe-framework](https://github.com/silverstripe/silverstripe-framework)

## Appendix B — Security training only

The following entries are suitable only for local labs, security education, or CTF-style practice. Do not deploy them to public servers.

- ethicalhack3r/DVWA

## Appendix C — Excluded from recommendations

Some original entries pointed to backdoors, webshells, private APIs, or other high-risk material. To keep this README safe and production-oriented, those entries are not linked or recommended.

- mgp25/Instagram-API — not recommended for application projects.
- owner888/phpspider — not recommended for application projects.
- bartblaze/PHP-backdoors — not recommended for application projects.
- JohnTroony/php-webshells — not recommended for application projects.
- nbs-system/php-malware-finder — not recommended for application projects.
- mgp25/SC-API — not recommended for application projects.

## Maintenance notes

- Review this README at least every three months.
- Recheck major releases for PHP, Laravel, Symfony, WordPress, Drupal, Joomla, PHPUnit, Pest, PHPStan, Rector, and Composer.
- When adding a new item, prefer this format: `Name | Package | Version line | Install | Use case | Status`.
- If a package becomes abandoned, archived, or security-risky, move it to the legacy/migration section.