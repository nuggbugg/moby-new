# MOBY Theme Development Notes

## Inventory Validation

**Important:** Shopify's `/products/handle.js` API does NOT expose inventory data (`inventory_quantity` and `inventory_policy` are always `undefined`).

**Solution:** Use Liquid to provide inventory data via data attributes on forms/buttons:
- `data-inventory-quantity="{{ variant.inventory_quantity }}"`
- `data-inventory-policy="{{ variant.inventory_policy }}"`

JavaScript then reads these data attributes for client-side validation instead of fetching from the API.

### Files with inventory validation:
- `sections/moby-buy-box.liquid` - Main product form
- `sections/moby-sticky-bar.liquid` - Sticky add to cart bar
- `snippets/moby-cart-drawer.liquid` - Cart drawer quantity controls
- `snippets/quantity-selector.liquid` - Quantity selector max attribute

## Brand Colors
- Dark: #1B1A0F
- Olive: #4F4A32
- Lime: #F9FDB5
- Sage: #C9C8B6

## Border Radius
- Capped at 6px across all components
