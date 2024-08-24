# よく使う WordPress 関数

-   記事一覧ページ
-   記事詳細ページ
-   お問い合わせページ
-   実績紹介ページ

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

### ★ページネーション

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

### ★カスタム投稿タイプ
製品を登録するためのカスタム投稿タイプを作り、そこに製品を登録していく

プラグインで実装する
#### Custom Post Type UI
https://ja.wordpress.org/plugins/custom-post-type-ui/

### ★カスタムフィールド
登録したそれぞれの製品に対して、情報を管理画面から追加するために必要  
- 値段
- 発売日
- サムネイル
- 説明文　など

プラグインで実装する
#### Advanced Custom Field
https://ja.wordpress.org/plugins/advanced-custom-fields/


