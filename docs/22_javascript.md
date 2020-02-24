# JavaScriptで動きをつける

スクロールした時にナビゲーションが表示されるなど動きを付けます。

base.htmlにJavaScriptを追記します。

blog/templates/blog/base.html

```html
  <script src="https://code.jquery.com/jquery-3.4.1.slim.min.js"></script>
  <script src="https://cdn.jsdelivr.net/npm/popper.js@1.16.0/dist/umd/popper.min.js"></script>
  <script src="https://stackpath.bootstrapcdn.com/bootstrap/4.4.1/js/bootstrap.min.js"></script>
  <script src="{% static 'js/blog.js' %}"></script>

</body>

</html>
```

blog/static/jsフォルダを作成します。

```
└── blog
    └── static
        └── js
            └── blog.js
```

blog.jsファイルを作成します。

JavaScript:blog/static/js/blog.js
```JavaScript:blog/static/js/blog.js
(function ($) {
  "use strict";

  $("body").on("input propertychange", ".floating-label-form-group", function (e) {
    $(this).toggleClass("floating-label-form-group-with-value", !!$(e.target).val());
  }).on("focus", ".floating-label-form-group", function () {
    $(this).addClass("floating-label-form-group-with-focus");
  }).on("blur", ".floating-label-form-group", function () {
    $(this).removeClass("floating-label-form-group-with-focus");
  });

  var MQL = 992;

  if ($(window).width() > MQL) {
    var headerHeight = $('#mainNav').height();
    $(window).on('scroll', {
      previousTop: 0
    },
      function () {
        var currentTop = $(window).scrollTop();
        if (currentTop < this.previousTop) {
          if (currentTop > 0 && $('#mainNav').hasClass('is-fixed')) {
            $('#mainNav').addClass('is-visible');
          } else {
            $('#mainNav').removeClass('is-visible is-fixed');
          }
        } else if (currentTop > this.previousTop) {
          $('#mainNav').removeClass('is-visible');
          if (currentTop > headerHeight && !$('#mainNav').hasClass('is-fixed')) {
            $('#mainNav').addClass('is-fixed');
          }
        }
        this.previousTop = currentTop;
      });
  }

})(jQuery);
```

スクロールすると、ナビゲーションに動きがつきました。
