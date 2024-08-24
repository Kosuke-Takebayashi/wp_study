## ＜jQueryの読み込み＞
WordPressにはデフォルトでjQueryが組み込まれているので
そちらを以下のようにして読み込む

```php
function my_enqueue_scripts() {
    // jQueryを登録してエンキュー
    wp_enqueue_script('jquery');
    
    // 自作のスクリプトをエンキューする例
    // wp_enqueue_script('my-custom-script', get_template_directory_uri() . '/assets/js/custom-script.js', array('jquery'), null, true);
}
add_action('wp_enqueue_scripts', 'my_enqueue_scripts');
```

<br>

WordPressでjQueryを使用する際は、「$」を「jQuery」にする
```javascript
jQuery(document).ready(function($) {
    jQuery('button').click(function() {
        alert('Button clicked!');
    });
});
```

