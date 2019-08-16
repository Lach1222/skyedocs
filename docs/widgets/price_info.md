# Price-info widget

## What is a widget?

A widget is a tag that will open a modal (a.k.a popup) when clicked. The content of the modal dialog provides additional information to the customer.

## How to use

To configure the widgets, simply copy the <script>..</script> tags below to your html content where you want them to appear and populate the highlighted fields (id, productPrice..etc.) with the correct values.

> Contact <a href="mailto:pit@%domain%">pit@%domain%</a> if you're unsure what type of merchant you are.

Insert the script where you want the price-info widget to display replacing <code>PLACE_YOUR_PRODUCT_PRICE</code> with the product price.

## Platform-specific Instructions
* [Shopify](/widgets/price-info/shopify)
* [Magetno 1](/widgets/price-info/magento_1)
* [OpenCart 3](/widgets/price-info/opencart_3)

## Skye price-info widgets

### Default widget

This widget displays the computed monthly installment amount.  The installment term used for computation is the longest term configured for the merchant in relation to the PRODUCT_PRICE provided.

Example: An amount of 2400 would automatically default to an 18 month term.

**Product price:** 2400

<script id="skye-widget" src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=D9168&amp;productPrice=2400" debug="true"></script>

```
<script id="skye-widget"src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=MERCHANT_CODE&productPrice=PRODUCT_PRICE"></script>
```

###Fixed term widget
This widget displays the computed installment amount against the provided term. This is ideal for promoting specific installment terms.

Example: An amount of 2500 would automatically default to an 18 month term. If merchant wants to promote 6 month terms, merchant just needs to supply the specific TERM  to the script.

**Product price:** 2500

<script id="skye-widget" src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=D9168&amp;productPrice=2500&amp;term=6" debug="true"></script>

```
<script id="skye-widget"src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=MERCHANT_CODE&price-selector=CSS_SELECTOR_URL_ENCODED&term=TERM"></script>
```

###Weekly widget
This widget displays the computed weekly installment amount. 

**Product price:** 700

<script id="skye-widget" src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=D9168&amp;productPrice=700&amp;mode=weekly" debug="true"></script>

```
<script id="skye-widget"src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=MERCHANT_CODE&productPrice=PRODUCT_PRICE&mode=weekly"></script>
```

## Widget features
### 1. Dynamically get product price

Instead of passing in a fixed ```productPrice``` value,  you can provide a ```price-selector``` query argument to target the HTML element containing the product price. Here, the price-info widget will get the product price from the specified element, and dynamically update when the price is changed.

If product price dynamically updateson user selection, or you have multiple products on the same page, the price-info widget can dynamically get the product price from a specified HTML element in the page.

With this feature, you can provide a **URL encoded** jQuery style CSS selector and it will bind a call back to the DOMSubTreeModified event.  
If the price is modified, it will update the payment info accordingly. 

For example, this is a block of HTML extracted from a typical WooCommerce product page:

```
<span>Product Price:</span>
<p class="price">
    <span id="priceinfo" class="woocommerce-Price-amount amount">
        <span class="woocommerce-Price-currencySymbol">$</span>900.00
    </span>
</p>
```

<p class="price">
    <span><strong>Product Price</strong>:</span>
    <span id="priceinfo" class="woocommerce-Price-amount amount">
        <span class="woocommerce-Price-currencySymbol">$</span>900.00
    </span>
</p>

In this case, we use the urlencoded ```%23priceinfo ``` to refer to the id ```#priceinfo```

<script id="skye-widget" src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=D9168&amp;price-selector=%23priceinfo&mode=weekly" debug="true"></script>


```
<script id="skye-widget"src="https://d1y94doel0eh42.cloudfront.net/content/scripts/skye-widget.js?id=MERCHANT_CODE&price-selector=CSS_SELECTOR_URL_ENCODED&mode=weekly"></script>
```

You could also use ```price-selector=.woocommerce-Price-amount.amount``` or any CSS selectors to help identify the price element.

### 2. Minimum and Maximum (Optional)

You may set the minimum and maximum prices the widget will display for by setting the ```data-min``` and ```data-max```  when calling the widget.

```
<script data-min="20" data-max="300" src="https://widgets.%domain%/content/scripts/price-info.js?productPrice=YOUR_PRICE"></script>
```
Here it will not display for prices above $300 or will display in an altered form for prices below $20.

<small>*We reserve the right to change any linked image at anytime without prior notice</small>
