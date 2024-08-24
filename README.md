# よく使う WordPress 関数

目次

-   記事一覧ページ
-   記事詳細ページ
-   お問い合わせページ
-   実績紹介ページ
-   リンクの設置方法
-   CSS や JS ファイルの読み込み方法

<br>

## ＜記事詳細ページ＞

### 記事タイトル

```php
the_title();
```

### 投稿日

https://thewppress.com/libraries/get-the-date/

```php
the_time();
```

※the_date()は同日の投稿の場合、連続で表示できない

### サムネイル

https://elearn.jp/wpman/function/the_post_thumbnail.html#google_vignette

```php
the_post_thumbnail( 'post-thumbnail', 'class=hoge' );
```

第二引数にクラス名を指定できる、サイズは CSS で調整

### カテゴリー

https://bambooworks.co/wordpress-category-show-only-one/

```php
$category = get_the_category();
  if ( $category[0] ) { // カテゴリーが登録されているとき
    echo '<a href="' . get_category_link( $category[0]->term_id ) . '">' . $category[0]->cat_name . '</a>';
  }
```

カテゴリーは複数登録できるが、一つだけを出力する場合が多い  
配列の 0 番目を出力している

### 記事本文

https://tcd-theme.com/2023/12/wp-the-content.html

```php
the_content();
```

<br>

## ＜記事一覧ページ＞

記事一覧、投稿日、記事タイトル、カテゴリーは記事詳細ページと同じ

### ★ ページネーション

https://www.conoha.jp/lets-wp/wp-pagination/#section07:~:text=box%2Dshadow%3A%20none%3B%0A%7D-,%E5%9B%BA%E5%AE%9A%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%A7%E5%AE%9F%E8%A3%85%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95,-%E5%9B%BA%E5%AE%9A%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AE

```php

// 固定ページの場合、これが必要
$paged = ( get_query_var( 'paged' ) ) ? absint( get_query_var( 'paged' ) ) : 1; // ※１

$args = array(
	// 各パラメータを設定

	'paged' => $paged, // ここにセットする
);

$the_query = new WP_Query( $args );

// WordPressのループ
// ~
// ループ終了

echo paginate_links(
    'total' => $the_query->max_num_pages, // 最大ページ数 $the_queryは上の変数名と合わせる
    'mid_size' => 1, // 現在のページの横にいくつ表示させるか
    'current' => ($paged ? $paged : 1), // 現在ページの番号
    'prev_text' => '< 前へ', // 前のページへののテキスト
    'next_text' => '次へ >', // 次のページへのテキスト
);
```

ページによって実装方法が少し異なるので注意  
※１を忘れがちなので注意

<br>

## ＜お問い合わせページ＞

プラグインで対応する

### ★Contact Form 7

https://ja.wordpress.org/plugins/contact-form-7/  
コードを書いて自由に設置できる

### ★Snow monkey forms

https://ja.wordpress.org/plugins/snow-monkey-forms/  
ブロックエディターで設置できる

<br>

## ＜実績紹介ページ＞

例えば、製品一つ一つを紹介するページでは、管理画面を少しカスタマイズする必要がある

### ★ カスタム投稿タイプ

製品を登録するためのカスタム投稿タイプを作り、そこに製品を登録していく

プラグインで実装する

#### Custom Post Type UI

https://ja.wordpress.org/plugins/custom-post-type-ui/

### ★ カスタムフィールド

登録したそれぞれの製品に対して、情報を管理画面から追加するために必要

-   値段
-   発売日
-   サムネイル
-   説明文　など

プラグインで実装する

#### Advanced Custom Field

https://ja.wordpress.org/plugins/advanced-custom-fields/

<br>

## リンクの設置方法

home_url()を使う  
https://tcd-theme.com/2023/12/wp-home-url.html#:~:text=%E3%81%AB%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82-,%E4%B8%8B%E5%B1%A4%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AEURL%E3%82%92%E5%8F%96%E5%BE%97%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95,-home_url()%E3%81%AF%E3%80%81%E3%83%88%E3%83%83%E3%83%97%E3%83%9A%E3%83%BC%E3%82%B8

```php
// 固定ページのスラッグが「test-page」の場合
echo esc_url( home_url( '/test-page' ) );

// 出力結果
// https://example.com/test-page
```

a タグでリンクを設置するときは次のように使う

```php
<a href="<?php echo esc_url( home_url( '/test-page' ) ) ?>">
```

<br>

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
