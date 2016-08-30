# Laravel-Mediable

[![Travis](https://img.shields.io/travis/plank/laravel-mediable/master.svg?style=flat-square)](https://travis-ci.org/plank/laravel-mediable)
[![Coveralls](https://img.shields.io/coveralls/plank/laravel-mediable.svg?style=flat-square)](https://coveralls.io/github/plank/laravel-mediable)
[![SensioLabsInsight](https://img.shields.io/sensiolabs/i/0eaf2725-64f4-4494-ae61-ca3961ba50c5.svg?style=flat-square)](https://insight.sensiolabs.com/projects/0eaf2725-64f4-4494-ae61-ca3961ba50c5)
[![StyleCI](https://styleci.io/repos/63791110/shield)](https://styleci.io/repos/63791110)
[![Packagist](https://img.shields.io/packagist/v/plank/laravel-mediable.svg?style=flat-square)](https://packagist.org/packages/plank/laravel-mediable)

Laravel-Mediable là một gói tập tin dễ dàng cho phép upload và gắn tập tin vào các model trog laravel 5.


## Features

- Filesystem-driven phương pháp tiếp cận cho phép dễ dàng tải nên bất kỳ số lượng file dễ dàng cấu hình để cho phép tải lên đến nhiều số lượng các thư mục với khả năng tiếp cận khác nhau.
- Many-to-many  mối quan hệ nhiều nhiêu cho phép bất kỳ số lượng media file tải lên được giao cho bất kỳ một model "bảng dữ liệu"  mà không cần sửa đổi "schema"  cấu trúc bảng dữ liệu.
- Gán media tới các model mở rộng gán thẻ tag. cho phép thiết lập và để lấy media file cho các mục đích khác nhau `thumbnail`,`avata`,`abum`,`featured image`,`gallery'` or `'download`.
- Dễ dàng truy vấn media file và uploads hạn chế "Mime Type " của file và đuôi mở rộng "extensionsEasily"  hoặc cả 2  "extension and/or" trong thống kê danh sách "aggregate type"

## Example Usage

Ví dụ sử dụng :

Upload 1 file từ server và nơi ở trong 1 thư mục của hệ thống quản lý tập tin như names disk "uploads" trong filesystem disk.
Điều này tạo ra một media ghi chép sử dụng để tham khảo tới file.


```php
$media = MediaUploader::fromSource($request->file('thumb'))
	->toDestination('uploads', 'blog/thumbnails')
	->upload();
```



Đính kèm media cho một mối quan hệ với bảng model với một mối quan hệ và định nghĩa thẻ tag cho mối quan hệ đó

Bạn có thể đính kèm media cho model của bạn giống như môt ví dụ sau : 

```php
$post = Post::create($this->request->input());
$post->attachMedia($media, ['thumbnail']);
```

Bạn có thể đính nhiều file cho một model bằng $media1->getKey() với 1 thẻ tag :

$post->attachMedia([$media1->getKey(), $media2->getKey()], 'gallery');

Hoặc ngược lại :

$post->attachMedia($media, ['gallery', 'featured']);



Gắn các  media tới  model với 1 thẻ tag(s).

```php
$post->getMedia('thumbnail')->first()->getUrl();
```

## Installation

Add the package to your Laravel app using composer

```bash
composer require plank/laravel-mediable
```

Register the package's servive provider in `config/app.php`

```php
'providers' => [
    ...
    'Plank\Mediable\MediableServiceProvider',
    ...
];
```

The package comes with a Facade for the image uploader, which you can optionally register as well.

```php
'aliases' => [
	...
    'MediaUploader' => 'Plank\Mediable\MediaUploaderFacade',
    ...
]
```

Publish the config file (`config/mediable.php`) and migration file (`database/migrations/####_##_##_######_create_mediable_tables.php`) of the package using artisan.

```bash
php artisan vendor:publish --provider="Plank\Mediable\MediableServiceProvider"
```

Run the migrations to add the required tables to your database.

```bash
php artisan migrate
```

## Documentation

Read the documentation [here](http://laravel-mediable.readthedocs.io/en/latest/).

## License

This package is released under the MIT license (MIT).

## About Plank

[Plank](http://plankdesign.com) is a web development agency based in Montreal, Canada.

