# Developer Technical Tasks
Technical tasks for developers to implement ecommerce data tracking, UX functionality, structured data, etc.

## eCommerce Tracking
Ensure the website pushes properly structured eCommerce data into the dataLayer for Google Analytics 4 tracking. This includes product views, add to cart, checkout steps, and purchase confirmation.

### Data Layer Format Specification

All eCommerce interactions should push data to the window.dataLayer using dataLayer.push() calls that match GA4 eCommerce schema.

Make sure any value contains the actual value with all the discounts and price drops.

Each dataLayer.push() should contain:
```
{
  event: "[event_name]",
  ecommerce: {
    currency: "[currency_code]",
    value: [total_value],
    items: [
      {
        item_id: "[sku or id]",
        item_name: "[product name]",
        item_brand: "[brand]",
        item_category: "[category]",
        affiliation: "Real French Food",
        price: [unit_price],
        quantity: [number]
      }
    ]
  }
}
```

### Required Events & Data Pushes

#### a. view_item

When: On product page
Push Example:
```
dataLayer.push({
  event: "view_item",
  ecommerce: {
    currency: "GBP",
    value: 49.99,
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 1
    }]
  }
});
```

#### b. add_to_cart

When: When user adds product to cart
Push Example:
```
dataLayer.push({
  event: "add_to_cart",
  ecommerce: {
    currency: "GBP",
    value: 49.99,
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 1
    }]
  }
});
```

#### c. view_cart

When: When user views a cart URL
Push Example:
```
dataLayer.push({
  event: "view_cart",
  ecommerce: {
    currency: "GBP",
    value: 99.98,
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 2
    }]
  }
});
```

#### d. remove_from_cart

When: When a user removes a product from the cart
Push Example:
```
dataLayer.push({
  event: "remove_from_cart",
  ecommerce: {
    currency: "GBP",
    value: 99.98,
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 2
    }]
  }
});
```

#### e. begin_checkout

When: On checkout page
Push Example:
```
dataLayer.push({
  event: "begin_checkout",
  ecommerce: {
    currency: "GBP",
    value: 99.98,
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 2
    }]
  }
});
```

#### f. add_shipping_info

When: On checkout start page
Push Example:
```
dataLayer.push({
  event: "add_shipping_info",
  ecommerce: {
    currency: "GBP",
    value: 99.98,
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 2
    }]
  }
});
```

#### g. add_payment_info

When: When a user submits their payment information (step 3+)
Push Example:
```
dataLayer.push({
  event: "add_payment_info",
  ecommerce: {
    currency: "GBP",
    value: 99.98,
    payment_type: "Credit Card",
    items: [{
      item_id: "SKU123",
      item_name: "Lindt Excellence Dark 85% 100g",
      item_brand: "Lindt",
      item_category: "Chocolate",
      affiliation: "Real French Food",
      price: 49.99,
      quantity: 2
    }]
  }
});
```

#### h. purchase

When: After successful order on confirmation page
Push Example:
```
dataLayer.push({
  event: "purchase",
  ecommerce: {
    transaction_id: "ORDER123",
    value: 109.98,
    currency: "GBP",
    payment_type: "Credit Card",
    items: [
      {
        item_id: "SKU123",
        item_name: "Lindt Excellence Dark 85% 100g",
        item_brand: "Lindt",
        item_category: "Chocolate",
        affiliation: "Real French Food",
        price: 49.99,
        quantity: 2
      }
    ]
  }
});
```

### Developer Notes

Place each dataLayer.push() before GA4 tag or GTM fires for the respective event.
Ensure values (currency, price, tax, etc.) are passed dynamically from the backend or JavaScript context.
