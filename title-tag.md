## ＜ title タグの設定＞

title タグは、header.php に直接書かないほうがよい  
その他 SEO 関連のタグは書かない方が良い

<br>

-   add_theme_support('title-tag')を使う
-   SEO プラグインを導入する  
    <br>

上のどちらかで対応する

<br>

### add_theme_support('title-tag')を使う

以下を書くことで、自動で出力してくれる

```php
// functions.phpに書く
function my_theme_setup() {
    add_theme_support('title-tag');
}
add_action('after_setup_theme', 'my_theme_setup');
```

<br>

### SEO プラグインを導入する

こちらの方が簡単でカスタマイズしやすい

<br>

Yoast SEO  
https://ja.wordpress.org/plugins/wordpress-seo/

SEO SIMPLE PACK  
https://ja.wordpress.org/plugins/seo-simple-pack/

All In One SEO  
https://ja.wordpress.org/plugins/all-in-one-seo-pack/
