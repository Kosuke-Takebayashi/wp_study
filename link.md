## ＜リンクの設置方法＞

home_url()を使う  
https://tcd-theme.com/2023/12/wp-home-url.html#:~:text=%E3%81%AB%E3%81%AA%E3%82%8A%E3%81%BE%E3%81%99%E3%80%82-,%E4%B8%8B%E5%B1%A4%E3%83%9A%E3%83%BC%E3%82%B8%E3%81%AEURL%E3%82%92%E5%8F%96%E5%BE%97%E3%81%99%E3%82%8B%E6%96%B9%E6%B3%95,-home_url()%E3%81%AF%E3%80%81%E3%83%88%E3%83%83%E3%83%97%E3%83%9A%E3%83%BC%E3%82%B8

```php
// 固定ページのスラッグが「test-page」の場合
echo esc_url( home_url( '/test-page' ) );

// 出力結果
// https://example.com/test-page
```

各ページへのリンクは、次のように書く

```php
<a href="<?php echo esc_url( home_url( '/test-page' ) ) ?>">
```