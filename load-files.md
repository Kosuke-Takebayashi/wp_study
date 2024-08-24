## ＜ CSS や JS ファイルの読み込み方法＞

link タグに直接書くのではなく、functions.php から読み込ませる  
「wp_enqueue_scripts」にフックさせる

```php
function my_scripts() {
     // linkタグ内に出力
     wp_enqueue_script( 'my-script', 'main.js', '', '1.0.0', false );
 }
 add_action('wp_enqueue_scripts', 'my_scripts');
```

<br>

ページを限定して読み込むことができる  
例えば、トップページでテーマフォルダ直下にある style.css を読み込みたい時は以下のようになる

```php
unction enqueue_my_custom_styles() {
    if (is_front_page() || is_home()) {
        wp_enqueue_style('my-style', get_stylesheet_uri());
    }
}
add_action('wp_enqueue_scripts', 'enqueue_my_custom_styles');
```

<br>
その他にも、以下のようなページを限定する関数が用意されている

```php
// 固定ページのみ
if(is_page()) {

}

// 固定ページのスラッグがcontactのページのみ
if(is_page('contact')) {

}

// 投稿ページのみ
if(is_single()) {

}

// 固定ページと投稿ページ
if(is_page() || is_single()) {

}

// その他、さまざまなページ指定ができる

```

<br>
例えば、以下のような構成の場合
- ヘッダーなどの全ページで共通のCSS・・・common.css、
- トップページ・・・style.css
- お問い合わせページ・・・contact.css

次のようなコードになる、

```php
function enqueue_my_custom_styles() {
    // 共通のCSSを全ページで読み込む
    wp_enqueue_style('common-style', get_template_directory_uri() . '/assets/css/common.css');

    // トップページのみでstyle.cssを読み込む
    if (is_front_page() || is_home()) {
        wp_enqueue_style('front-page-style', get_template_directory_uri() . '/style.css');
    }

    // お問い合わせページ（例: slugが'contact'であるページ）でcontact.cssを読み込む
    if (is_page('contact')) {
        wp_enqueue_style('contact-page-style', get_template_directory_uri() . '/assets/css/contact.css');
    }
}
add_action('wp_enqueue_scripts', 'enqueue_my_custom_styles');

```