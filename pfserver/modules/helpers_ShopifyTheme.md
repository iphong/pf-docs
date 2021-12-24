[PF Server](../README.md) / helpers/ShopifyTheme

# Module: helpers/ShopifyTheme

## Table of contents

### Variables

- [blogCSS](helpers_ShopifyTheme.md#blogcss)
- [defaultShopifyIndex](helpers_ShopifyTheme.md#defaultshopifyindex)
- [hideHeaderFooterTemplate](helpers_ShopifyTheme.md#hideheaderfootertemplate)
- [pageflyArticleInfo](helpers_ShopifyTheme.md#pageflyarticleinfo)
- [pageflyArticleTags](helpers_ShopifyTheme.md#pageflyarticletags)
- [pageflyCollectionBackup](helpers_ShopifyTheme.md#pageflycollectionbackup)
- [pageflyCommentForm](helpers_ShopifyTheme.md#pageflycommentform)
- [pageflyFeaturedImage](helpers_ShopifyTheme.md#pageflyfeaturedimage)
- [pageflyProductBackup](helpers_ShopifyTheme.md#pageflyproductbackup)
- [pageflyProductBackupOld](helpers_ShopifyTheme.md#pageflyproductbackupold)
- [pageflyTranslation](helpers_ShopifyTheme.md#pageflytranslation)
- [pfComment](helpers_ShopifyTheme.md#pfcomment)
- [showLinkPasswordPageSnippet](helpers_ShopifyTheme.md#showlinkpasswordpagesnippet)

### Functions

- [addMainStyleToTheme](helpers_ShopifyTheme.md#addmainstyletotheme)
- [addPageFlySettingSnippetToTheme](helpers_ShopifyTheme.md#addpageflysettingsnippettotheme)
- [generateGSCSS](helpers_ShopifyTheme.md#generategscss)
- [removeAlertFromHTML](helpers_ShopifyTheme.md#removealertfromhtml)
- [removeAllScriptFromHTML](helpers_ShopifyTheme.md#removeallscriptfromhtml)
- [removePageFlyPreviewShortCode](helpers_ShopifyTheme.md#removepageflypreviewshortcode)
- [updatePageFlySnippetToShopify](helpers_ShopifyTheme.md#updatepageflysnippettoshopify)
- [updateThemeTranslation](helpers_ShopifyTheme.md#updatethemetranslation)

## Variables

### blogCSS

• **blogCSS**: ``".pf-article__tags,\n.pf-article__comment {\n  background-color: #fff;\n  padding: 30px 0;\n}\n.pf-article__tags ul,\n.pf-article__comment ul {\n  margin: 0;\n  padding: 0;\n}\n\n.pf-article__header {\n  text-align: center;\n  padding: 20px 15px 30px;\n}\n.pf-article__header h1 {\n  margin-bottom: 10px;\n}\n.pf-article__header .pf-article__author {\n  margin-right: 10px;\n}\n\n.pf-article__image {\n  margin-bottom: 30px;\n  text-align: center;\n}\n\n.pf-comment__list {\n  margin-bottom: 30px;\n}\n\n.pf-comment__form label {\n  display: block;\n  margin-bottom: 10px;\n}\n.pf-comment__form input:not([type=submit]), .pf-comment__form textarea {\n  width: 100%;\n}\n\n.pf-article__tags li {\n  list-style: none;\n  display: inline-block;\n  margin-right: 10px;\n}\n.pf-article__tags li a {\n  display: inline-block;\n  padding: 5px 10px;\n  background-color: #f5f5f5;\n}\n.pf-article__tags + .pf-article__comment {\n  padding-top: 0;\n}\n\n.pf-comment__list li {\n  list-style: none;\n  margin-bottom: 30px;\n}\n.pf-comment__list li:last-child {\n  margin-bottom: 0;\n}\n\n.pf-comment__author {\n  margin-bottom: 10px;\n  padding-bottom: 10px;\n  border-bottom: 1px solid #ebebeb;\n}\n.pf-comment__author > span {\n  padding-right: 15px;\n  font-weight: 700;\n}"``

#### Defined in

[src/helpers/ShopifyTheme.ts:239](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-239)

___

### defaultShopifyIndex

• **defaultShopifyIndex**: ``"{{ content_for_index }}"``

#### Defined in

[src/helpers/ShopifyTheme.ts:233](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-233)

___

### hideHeaderFooterTemplate

• **hideHeaderFooterTemplate**: ``"{% layout 'theme.pagefly' %}\n"``

#### Defined in

[src/helpers/ShopifyTheme.ts:14](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-14)

___

### pageflyArticleInfo

• **pageflyArticleInfo**: ``"{% if article.author != blank and article.title != blank %}<div class=\"pf-arh\" style=\"text-align: center;padding:20px 15px 30px;\"><h1 style=\"margin: 0 0 10px\">{{ article.title }}</h1><div><span style=\"margin-right:10px\">{{ 'pagefly.article.by_author' | t: author: article.author }}</span><time datetime=\"{{ article.published_at | date: \"%b %d, %Y\" }}\">{{ article.published_at | date: \"%b %d, %Y\" }}</time></div></div>{% endif %}"``

#### Defined in

[src/helpers/ShopifyTheme.ts:227](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-227)

___

### pageflyArticleTags

• **pageflyArticleTags**: ``"{% if article.tags.size > 0 %}<div class=\"pf-art\" style=\"margin-top:30px;\"><div style=\"max-width:1170px;margin:auto;width:100%;padding:0 15px;\"><h3>{{ 'pagefly.article.tags' | t }}</h3><div class=\"pf-r-dg\" style=\"grid-auto-columns: max-content;grid-auto-flow: column;grid-gap: 10px;\">{% for tag in article.tags %}<a style=\"padding:5px 10px;background:#f5f5f5;color:#000\" href=\"{{ blog.url }}/tagged/{{ tag | handle }}\">{{ tag }}</a>{% endfor %}</div></div></div>{% endif %}"``

#### Defined in

[src/helpers/ShopifyTheme.ts:229](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-229)

___

### pageflyCollectionBackup

• **pageflyCollectionBackup**: ``"templates/collection.pagefly-backup.liquid"``

#### Defined in

[src/helpers/ShopifyTheme.ts:237](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-237)

___

### pageflyCommentForm

• **pageflyCommentForm**: ``"{%- assign new_comment = false -%}{% if comment and comment.created_at %}{%- assign new_comment = true -%}{%- assign new_comment_id = comment.id -%}{% endif %}{% if new_comment %}{%- assign duplicate_comment = false %}{% for comment in article.comments %}{% if comment.id == new_comment_id %}{%- assign duplicate_comment = true %}{% break %}{% endif %}{% endfor %}{% if duplicate_comment %}{%- assign number_of_comments = article.comments_count -%}{% else %}{%- assign number_of_comments = article.comments_count | plus: 1 -%}{% endif %}{% else %}{%- assign number_of_comments = article.comments_count -%}{% endif %}{% capture pagefly_comment %}<div style=\"border-bottom:1px solid #ebebeb;margin-bottom:10px;padding-bottom:10px;\"><span style=\"margin-right:15px;font-weight:bold\">{{ comment.author }}</span><small>{{ comment.created_at | date: \"%b %d, %Y\" }}</small></div>{{ comment.content }}{% endcapture %}{% if blog.comments_enabled? %}<div class=\"pf-arc\" style=\"margin-top:30px;\"><div style=\"max-width:1170px;margin:auto;width:100%;padding:0 15px;\">{% if number_of_comments > 0 %}<div style=\"margin-bottom:30px\"><h3>{{ 'pagefly.comments.comments_with_count' | t: count: number_of_comments }}</h3>{% paginate article.comments by 5 %}{% comment %}#comments is required, it is used as an anchor link by Shopify.{% endcomment %}{% if new_comment %}<p class=\"note form-success\">{% if blog.moderated? %}{{ 'pagefly.comments.success_moderated' | t }}{% else %}{{ 'pagefly.comments.success' | t }}{% endif %}</p>{% endif %}<ul class=\"comments\">{% comment %}If a comment was just submitted with no blank field, show it.{% endcomment %}{% if new_comment %}{% unless paginate.current_page > 1 %}<li id=\"comment-{{ comment.id }}\" class=\"comment\">{{ pagefly_comment }}</li>{% endunless %}{% endif %}{% for comment in article.comments %}{% unless comment.id == new_comment_id %}<li id=\"comment-{{ comment.id }}\" class=\"comment\"><div style=\"border-bottom:1px solid #ebebeb;margin-bottom:10px;padding-bottom:10px;\"><span style=\"margin-right:15px;font-weight:bold\">{{ comment.author }}</span><small>{{ comment.created_at | date: \"%b %d, %Y\" }}</small></div>{{ comment.content }}</li>{% endunless %}{% endfor %}</ul>{% if paginate.pages > 1 %}<div class=\"pf-pagination\">{{ paginate | default_pagination | replace: '&laquo; Previous', '&larr;' | replace: 'Next &raquo;', '&rarr;' }}</div>{% endif %}{% endpaginate %}</div>{% endif %}{% form 'new_comment', article %}<h3>{{ 'pagefly.comments.title' | t }}</h3>{{ form.errors | default_errors }}<div class=\"pf-r\"><div class=\"pf-c pf-c-xs--12 pf-c-lg--6\"><label for='CommentAuthor'>{{ 'pagefly.comments.name' | t }}</label><input style=\"width:calc(100% - 15px)\" type='text' name='comment[author]' id='CommentAuthor' class='input-full{% if form.errors contains 'author' %} input--error{% endif %}' value='{{ form.author }}'></div><div class=\"pf-c pf-c-xs--12 pf-c-lg--6\"><label for='CommentEmail'>{{ 'pagefly.comments.email' | t }}</label><input style=\"width:calc(100% - 15px);margin-left:15px;\" type='email' name='comment[email]' id='CommentEmail' class='input-full{% if form.errors contains 'email' %} input--error{% endif %}' value='{{ form.email }}' autocorrect='off' autocapitalize='off'></div><div class=\"pf-c pf-c-xs--12 pf-c-lg--12\" style=\"margin:30px 0\"><label for='CommentBody'>{{ 'pagefly.comments.message' | t }}</label><textarea style=\"width:100%\" name='comment[body]' id='CommentBody' class='input-full{% if form.errors contains 'body' %} input--error{% endif %}'>{{ form.body }}</textarea></div><div class=\"pf-c pf-c-xs--12 pf-c-lg--12\">{% if blog.moderated? %}<p class='fine-print'>{{ 'pagefly.comments.moderated' | t }}</p>{% endif %}<input type='submit' class='btn' value='{{ 'pagefly.comments.post' | t }}'></div></div>{% endform %}</div></div>{% endif %}"``

#### Defined in

[src/helpers/ShopifyTheme.ts:225](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-225)

___

### pageflyFeaturedImage

• **pageflyFeaturedImage**: ``"{% if article.image %}<div class=\"pf-ari\" style=\"margin-bottom:30px\"><div style=\"max-width:1170px;margin:auto;width:100%;padding:0 15px;\"><img loading='lazy' src='{{ article | img_url: 'master' }}' alt='{{ article.title }}' /></div></div>{% endif %}"``

#### Defined in

[src/helpers/ShopifyTheme.ts:231](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-231)

___

### pageflyProductBackup

• **pageflyProductBackup**: ``"templates/product.pagefly-backup.liquid"``

#### Defined in

[src/helpers/ShopifyTheme.ts:235](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-235)

___

### pageflyProductBackupOld

• **pageflyProductBackupOld**: ``"templates/product.pagefly.backup.liquid"``

#### Defined in

[src/helpers/ShopifyTheme.ts:236](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-236)

___

### pageflyTranslation

• **pageflyTranslation**: `Object`

#### Type declaration

| Name | Type |
| :------ | :------ |
| `article` | `Object` |
| `article.all_topics` | `string` |
| `article.back_to_blog` | `string` |
| `article.by_author` | `string` |
| `article.posted_in` | `string` |
| `article.read_more` | `string` |
| `article.tags` | `string` |
| `comments` | `Object` |
| `comments.comments_with_count` | `Object` |
| `comments.comments_with_count.one` | `string` |
| `comments.comments_with_count.other` | `string` |
| `comments.email` | `string` |
| `comments.message` | `string` |
| `comments.moderated` | `string` |
| `comments.name` | `string` |
| `comments.post` | `string` |
| `comments.success` | `string` |
| `comments.success_moderated` | `string` |
| `comments.title` | `string` |
| `password_page` | `Object` |
| `password_page.login_form_message` | `string` |
| `password_page.login_form_password_label` | `string` |
| `password_page.login_form_password_placeholder` | `string` |
| `password_page.login_form_submit` | `string` |
| `password_page.password_link` | `string` |
| `password_page.signup_form_email_label` | `string` |
| `password_page.signup_form_success` | `string` |
| `products` | `Object` |
| `products.product` | `Object` |
| `products.product.add_to_cart` | `string` |
| `products.product.back_to_collection` | `string` |
| `products.product.on_sale` | `string` |
| `products.product.quantity` | `string` |
| `products.product.regular_price` | `string` |
| `products.product.sold_out` | `string` |
| `products.product.unavailable` | `string` |
| `products.product.view_details` | `string` |

#### Defined in

[src/helpers/ShopifyTheme.ts:39](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-39)

___

### pfComment

• **pfComment**: ``"{% comment %}\nThis file is auto-generated by PageFly. The content can be overridden when publish page in PageFly. Please do not update this file directly.\nIf you plan to remove PageFly, please see the guide in our help center first: https://help.pagefly.io/.\n{% endcomment %}\n"``

#### Defined in

[src/helpers/ShopifyTheme.ts:9](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-9)

___

### showLinkPasswordPageSnippet

• **showLinkPasswordPageSnippet**: ``"\n<div class=\"__pf_password\">\n    <a href=\"#\" class=\"__pf_password-btn\">{{ 'pagefly.password_page.password_link' | t }}</a>\n\n    <div class=\"__pf_password-form\">\n        {% form \"storefront_password\" %}\n        {{ form.errors | default_errors }}\n        <p>{{ 'pagefly.password_page.login_form_message' | t }}</p>\n        <div>\n            <input type=\"password\" name=\"password\" placeholder=\"{{ 'pagefly.password_page.login_form_password_placeholder' | t }}\">\n            <input type=\"submit\" value=\"{{ 'pagefly.password_page.login_form_submit' | t }}\">\n        </div>\n        {% endform %}\n\n        <span class=\"__pf_password-form--close\"></span>\n    </div>\n\n    <style>\n        .__pf_password-btn {\n            position: fixed;\n            right: 10px;\n            top: 10px;\n            padding: 10px 20px;\n            background: #000;\n            border: 1px solid #333;\n            text-transform: uppercase;\n            font-size: 10px;\n            letter-spacing: 2px;\n            font-weight: bold;\n            z-index: 100;\n            color: #fff;\n        }\n        .__pf_password-btn:hover {\n            color: #fff !important;\n            text-decoration: none !important;\n            background: #222;\n        }\n        .__pf_password-form {\n            display: none;\n            justify-content: center;\n            align-items: center;\n            position: fixed;\n            width: 100%;\n            height: 100%;\n            background: rgba(0, 0, 0, .8);\n            z-index: 10;\n            top: 0;\n        }\n        .__pf_password-form form {\n            max-width: 100%;\n            background: #fff;\n            padding: 30px 20px;\n            border-radius: 2px;\n            width: 480px;\n            text-align: center;\n        }\n        .__pf_password-form form > div {\n            position: relative;\n        }\n        .__pf_password-form form p {\n            color: #000;\n            font-size: 18px;\n            margin: 0 0 20px;\n        }\n        .__pf_password-form form label {\n            margin-bottom: 10px;\n        }\n        .__pf_password-form input[type=\"password\"] {\n            border: 1px solid #bfbfbf;\n            outline: 0;\n            border-radius: 2px;\n            height: 50px;\n            padding: 0 20px;\n            line-height: 50px;\n            width: 100%;\n        }\n        .__pf_password-form input[type=\"submit\"] {\n            position: absolute;\n            height: 42px;\n            min-height: initial;\n            line-height: 1;\n            padding: 0 20px;\n            background: #000;\n            color: #fff;\n            top: 4px;\n            right: 4px;\n            border-radius: 2px;\n            -webkit-appearance: none;\n            outline: 0;\n            border: 0;\n            width: fit-content;\n        }\n        .__pf_password-form input[type=\"submit\"]:hover {\n            opacity: .8;\n        }\n        .__pf_password-form--close {\n            width: 50px;\n            height: 50px;\n            cursor: pointer;\n            display: block;\n            position: absolute;\n            right: 20px;\n            top: 20px;\n        }\n        .__pf_password-form--close:before,\n        .__pf_password-form--close:after {\n            content: \"\";\n            width: 30px;\n            height: 1px;\n            background: #fff;\n            position: absolute;\n            top: 24px;\n            left: 11px;\n        }\n        .__pf_password-form--close:before {\n            transform: rotate(45deg);\n        }\n        .__pf_password-form--close:after {\n            transform: rotate(-45deg);\n        }\n    </style>\n\n    <script>\n        window.addEventListener(\"load\", function() {\n            document.querySelector(\".__pf_password-btn\").addEventListener(\"click\", function() {\n                document.querySelector(\".__pf_password-btn\").style.display = \"none\";\n                document.querySelector(\".__pf_password-form\").style.display = \"flex\";\n            });\n            document.querySelector(\".__pf_password-form--close\").addEventListener(\"click\", function() {\n                document.querySelector(\".__pf_password-form\").style.display = \"none\";\n                document.querySelector(\".__pf_password-btn\").style.display = \"initial\";\n            });\n            if ( document.querySelectorAll(\".errors\").length ) {\n                document.querySelector(\".__pf_password-btn\").click();\n            }\n        });\n    </script>\n</div>"``

#### Defined in

[src/helpers/ShopifyTheme.ts:86](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-86)

## Functions

### addMainStyleToTheme

▸ `Const` **addMainStyleToTheme**(`Shop`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/helpers/ShopifyTheme.ts:338](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-338)

___

### addPageFlySettingSnippetToTheme

▸ `Const` **addPageFlySettingSnippetToTheme**(`Shop`): `Promise`<`void` \| `IAsset`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`void` \| `IAsset`\>

#### Defined in

[src/helpers/ShopifyTheme.ts:455](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-455)

___

### generateGSCSS

▸ `Const` **generateGSCSS**(`__namedParameters`): `string`

#### Parameters

| Name | Type |
| :------ | :------ |
| `__namedParameters` | `Object` |

#### Returns

`string`

#### Defined in

[src/helpers/ShopifyTheme.ts:321](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-321)

___

### removeAlertFromHTML

▸ **removeAlertFromHTML**(`html?`): `string`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `html` | `string` | `''` |

#### Returns

`string`

#### Defined in

[src/helpers/ShopifyTheme.ts:492](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-492)

___

### removeAllScriptFromHTML

▸ **removeAllScriptFromHTML**(`html?`): `string`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `html` | `string` | `''` |

#### Returns

`string`

#### Defined in

[src/helpers/ShopifyTheme.ts:483](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-483)

___

### removePageFlyPreviewShortCode

▸ **removePageFlyPreviewShortCode**(`html?`): `string`

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `html` | `string` | `''` |

#### Returns

`string`

#### Defined in

[src/helpers/ShopifyTheme.ts:501](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-501)

___

### updatePageFlySnippetToShopify

▸ **updatePageFlySnippetToShopify**(`Shop`): `Promise`<`void`\>

#### Parameters

| Name | Type |
| :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/helpers/ShopifyTheme.ts:376](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-376)

___

### updateThemeTranslation

▸ `Const` **updateThemeTranslation**(`Shop`, `pfTranslation?`): `Promise`<`void`\>

#### Parameters

| Name | Type | Default value |
| :------ | :------ | :------ |
| `Shop` | [`PFShop`](../classes/data_models_Shop.PFShop.md) | `undefined` |
| `pfTranslation` | `Object` | `pageflyTranslation` |
| `pfTranslation.article` | `Object` | `undefined` |
| `pfTranslation.article.all_topics` | `string` | `"All topics"` |
| `pfTranslation.article.back_to_blog` | `string` | `"Back to {{ title }}"` |
| `pfTranslation.article.by_author` | `string` | `"by {{ author }}"` |
| `pfTranslation.article.posted_in` | `string` | `"Posted in"` |
| `pfTranslation.article.read_more` | `string` | `"Read more"` |
| `pfTranslation.article.tags` | `string` | `"Tags:"` |
| `pfTranslation.comments` | `Object` | `undefined` |
| `pfTranslation.comments.comments_with_count` | `Object` | `undefined` |
| `pfTranslation.comments.comments_with_count.one` | `string` | `"{{ count }} comment"` |
| `pfTranslation.comments.comments_with_count.other` | `string` | `"{{ count }} comments"` |
| `pfTranslation.comments.email` | `string` | `"Email"` |
| `pfTranslation.comments.message` | `string` | `"Message"` |
| `pfTranslation.comments.moderated` | `string` | `"Please note, comments must be approved before they are published"` |
| `pfTranslation.comments.name` | `string` | `"Name"` |
| `pfTranslation.comments.post` | `string` | `"Post comment"` |
| `pfTranslation.comments.success` | `string` | `"Your comment was posted successfully! Thank you!"` |
| `pfTranslation.comments.success_moderated` | `string` | `"Your comment was posted successfully. We will publish it in a little while, as our blog is moderated."` |
| `pfTranslation.comments.title` | `string` | `"Leave a comment"` |
| `pfTranslation.password_page` | `Object` | `undefined` |
| `pfTranslation.password_page.login_form_message` | `string` | `"Enter store using password:"` |
| `pfTranslation.password_page.login_form_password_label` | `string` | `"Password"` |
| `pfTranslation.password_page.login_form_password_placeholder` | `string` | `"Your password"` |
| `pfTranslation.password_page.login_form_submit` | `string` | `"Enter"` |
| `pfTranslation.password_page.password_link` | `string` | `"Enter using password"` |
| `pfTranslation.password_page.signup_form_email_label` | `string` | `"Email"` |
| `pfTranslation.password_page.signup_form_success` | `string` | `"We will send you an email right before we open!"` |
| `pfTranslation.products` | `Object` | `undefined` |
| `pfTranslation.products.product` | `Object` | `undefined` |
| `pfTranslation.products.product.add_to_cart` | `string` | `"Add to cart"` |
| `pfTranslation.products.product.back_to_collection` | `string` | `"Back to {{ title }}"` |
| `pfTranslation.products.product.on_sale` | `string` | `"Sale"` |
| `pfTranslation.products.product.quantity` | `string` | `"Quantity"` |
| `pfTranslation.products.product.regular_price` | `string` | `"Regular price"` |
| `pfTranslation.products.product.sold_out` | `string` | `"Sold out"` |
| `pfTranslation.products.product.unavailable` | `string` | `"Unavailable"` |
| `pfTranslation.products.product.view_details` | `string` | `"View details"` |

#### Returns

`Promise`<`void`\>

#### Defined in

[src/helpers/ShopifyTheme.ts:464](https://bitbucket.org/bravebits/pfserver/src/83cf3bb/src/helpers/ShopifyTheme.ts#lines-464)
