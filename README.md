Custom Ajax cart  1 -put UTcart.js to assets folder
2 - import UTcart.js, cart-drawer.css to theme.liquid   - At header

 <script src="{{ `UTcart.js` | asset_url }}" defer="defer"></script>
  {{ 'UTcart.css' | asset_url | stylesheet_tag }}  - At Body    {% render 'UTcart' %}  %- capture var -%}{ {% for product in collections['all'].products %}{% for   variant in product.variants %}"{{ variant.id }}":"{{     variant.inventory_quantity   }}-{{ variant.inventory_policy }}" cap={{ variant.compare_at_price }}{% unless forloop.last %},{% endunless   %}{% endfor %} {% endfor %} }{%- endcapture -%}   <script type="application/json" id="all_variant_track">     {{var | json}}   </script>

- Add to body in theme.liquid attribute: data-currencySymbol="{{ cart.currency.symbol }}"  3 - Copy settings from settings_schema.json and paste to config - settings_schema.json   3 - in header.liquid find cart icon and add onclick="openCart()" for parent container, replace <a> tag to <div>, remove href attribute, and add for span, id="cart_count" when use {{ cart.item_count }}




4 - Add UTcart.liquid to snippets folder, add cart-drawer.liquid and render previous file, then, render this file in theme.liquid
{% render 'UTcart' %}

5 - in main-product.liquid find quantity selector, ( default <quantity-input class="quantity"> ), inside input use attribute :

id="product_quantity-{{ product.selected_or_first_available_variant.id }}"

6 - under </quantity-input> paste:
  <div class="out_in_stock">Selected product quantity out in stock!</div>

7 - find type="submit" button, replace ‘submit’ to ‘button’, add attributes:

 onclick="handleAddToCart(this)"
 data-inputid="{{ product.selected_or_first_available_variant.id }}"

8 - find input by name=«id», paste id="varId-{{ product.selected_or_first_available_variant.id }}"






 

  