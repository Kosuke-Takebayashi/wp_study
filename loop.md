## その他の注意点

- 関数を使う際のフォールバック

<br>

### 関数を使う際のフォールバック
例えば、サムネイル画像を表示するときに、設定されていないケースを考慮して、if文で書いておく

<br>

以下は、設定されていないときにダミーの画像を出力する例

```php

if (has_post_thumbnail()) {
    // サムネイル画像が設定されている場合
    the_post_thumbnail(); // サイズは必要に応じて変更
} else {
    // サムネイル画像が設定されていない場合
    $fallback_image_url = get_template_directory_uri() . '/assets/images/fallback-image.jpg'; // フォールバック画像のパス
    echo '<img src="' . esc_url($fallback_image_url) . '" alt="Fallback Image">';
}

```