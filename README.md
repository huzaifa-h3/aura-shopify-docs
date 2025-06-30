# Aura - Shopify Theme Documentation

## Table of Contents
1. [Overview](#overview)
2. [Installation](#installation)
3. [Theme Structure](#theme-structure)
4. [JavaScript Modules](#javascript-modules)
5. [Features](#features)
6. [Configuration](#configuration)
7. [Customization](#customization)
8. [API Reference](#api-reference)
9. [Troubleshooting](#troubleshooting)
10. [Development](#development)

## Overview

Aura is a lightweight, modern Shopify theme designed for optimal performance and user experience. It features a modular JavaScript architecture, responsive design, and comprehensive e-commerce functionality.

### Key Features
- 🚀 Lightweight and fast-loading
- 📱 Fully responsive design
- 🛒 Advanced cart management
- 🔍 Real-time search functionality
- 💝 Wishlist integration
- 🎨 Collection filtering and sorting
- 📧 Contact form handling
- 🌍 Multi-currency support
- 📱 Mobile-optimized navigation

## Installation

1. Download the theme files
2. Upload to your Shopify admin under **Online Store > Themes**
3. Customize theme settings as needed
4. Publish the theme

## Theme Structure

```
assets/
├── theme.js              # Core theme functionality
├── cart.js               # Cart management
├── cart-drawer.js        # Sliding cart drawer
├── add-to-cart.js        # Add to cart system
├── collection-filtering.js # Product filtering
├── featured-collection.js # Featured products
├── search-overlay.js     # Search functionality
├── mobile-menu.js        # Mobile navigation
└── contact-form.js       # Contact form handling
```

## JavaScript Modules

### 1. Theme Core (`theme.js`)

The main theme file handles global functionality:

**Features:**
- Page preloading states
- Smooth scrolling for anchor links
- Scroll-based animations
- Performance optimization with debouncing

**Usage:**
```javascript
// Automatic initialization on DOMContentLoaded
// No manual setup required
```

### 2. Cart Management (`cart.js`)

Handles cart operations and quantity updates.

**Class:** `CartManager`

**Methods:**
- `handleQuantityChange(button)` - Updates item quantities
- `handleInputChange(input)` - Direct quantity input handling
- `handleRemoveItem(link)` - Removes items from cart
- `updateCart(itemId, quantity)` - Updates cart via AJAX

**HTML Structure:**
```html
<button class="quantity-btn" data-action="increase" data-id="VARIANT_ID">+</button>
<input class="quantity-input" data-id="VARIANT_ID" value="1">
<button class="quantity-btn" data-action="decrease" data-id="VARIANT_ID">-</button>
<a href="#" class="remove-items" data-id="VARIANT_ID">Remove</a>
```

### 3. Cart Drawer (`cart-drawer.js`)

Sliding cart drawer with multi-currency support.

**Class:** `CartDrawer`

**Features:**
- Real-time cart updates
- Multi-currency conversion
- Geolocation-based currency detection
- Smooth animations

**Supported Currencies:**
- USD (United States)
- PKR (Pakistan)
- INR (India)
- GBP (United Kingdom)
- CAD (Canada)
- AUD (Australia)
- AED (UAE)
- SAR (Saudi Arabia)
- BDT (Bangladesh)

**Methods:**
- `open()` - Opens the cart drawer
- `close()` - Closes the cart drawer
- `fetchCart()` - Updates cart contents
- `detectUserCountry()` - Auto-detects user location

### 4. Add to Cart System (`add-to-cart.js`)

Manages product additions to cart and wishlist.

**Class:** `AddToCartManager`

**Features:**
- AJAX cart additions
- Loading states
- Success notifications
- Wishlist integration
- Error handling

**HTML Structure:**
```html
<button class="add-to-cart-btn" 
        data-variant-id="VARIANT_ID" 
        data-product-title="PRODUCT_NAME">
  Add to Cart
</button>

<button class="wishlist-btn" data-product-id="PRODUCT_ID">
  Add to Wishlist
</button>
```

### 5. Collection Filtering (`collection-filtering.js`)

Advanced product filtering and sorting system.

**Function:** `collectionFiltering()`

**Features:**
- Multi-attribute filtering (availability, color, size)
- Real-time product count updates
- Sorting options
- Color swatch support
- Pagination

**Filter Types:**
- **Availability:** In stock, out of stock
- **Color:** Visual color swatches
- **Size:** Size variants
- **Sorting:** Manual, price, date, popularity

**Data Structure:**
```javascript
filters: {
  availability: [],
  color: [],
  size: []
}
```

### 6. Search Overlay (`search-overlay.js`)

Real-time search with suggestions and results.

**Features:**
- Instant search suggestions
- Debounced search queries
- Loading animations
- Keyboard navigation
- Mobile-optimized

**HTML Structure:**
```html
<div id="searchOverlay">
  <input id="searchInput" type="text" placeholder="Search...">
  <div id="searchSuggestions"></div>
  <div id="searchResultsContainer"></div>
</div>
```

### 7. Mobile Menu (`mobile-menu.js`)

Responsive mobile navigation system.

**Features:**
- Slide-in animations
- Multi-level navigation
- Touch-friendly interface
- Outside click detection

**HTML Structure:**
```html
<button id="mobile-menu-toggle">Menu</button>
<div id="mobileMenu">
  <button class="subMenuButton" data-target="submenu-1">Category</button>
  <div id="submenu-1">
    <button class="back-button" data-back="mobileMenu">Back</button>
  </div>
</div>
```

### 8. Contact Form (`contact-form.js`)

Enhanced contact form with validation and feedback.

**Features:**
- AJAX form submission
- Real-time validation
- Loading states
- Success/error messaging
- Form reset on success

## Configuration

### Cart Drawer Settings

```javascript
// Currency configuration
exchangeRates: {
  'US': { currency: 'USD', rate: 1, symbol: '$' },
  'PK': { currency: 'PKR', rate: 280, symbol: 'Rs.' },
  // Add more currencies as needed
}
```

### Collection Filtering Settings

```javascript
// Products per page
productsPerPage: 15,

// Default sort order
sortBy: 'manual',

// Filter visibility
openFilters: {
  availability: true,
  color: true,
  size: true
}
```

## Customization

### Adding New Currencies

1. Update the `exchangeRates` object in `cart-drawer.js`:

```javascript
exchangeRates: {
  'NEW_COUNTRY_CODE': { 
    currency: 'CURRENCY_CODE', 
    rate: EXCHANGE_RATE, 
    symbol: 'SYMBOL' 
  }
}
```

### Custom Color Swatches

Add new colors to the `colorMap` in `collection-filtering.js`:

```javascript
colorMap: {
  'custom-color': '#hexcode',
  // existing colors...
}
```

### Modifying Search Behavior

Customize search parameters in `search-overlay.js`:

```javascript
// Search delay (milliseconds)
const SEARCH_DELAY = 300;

// Minimum characters to trigger search
const MIN_SEARCH_LENGTH = 2;
```

## API Reference

### Cart API Endpoints

- `POST /cart/add.js` - Add items to cart
- `POST /cart/change.js` - Update cart quantities
- `GET /cart.js` - Get cart contents
- `POST /cart/clear.js` - Clear cart

### Search API

- `GET /search/suggest.json` - Get search suggestions
- `GET /search.json` - Get search results

## Troubleshooting

### Common Issues

**Cart not updating:**
- Check variant IDs are correct
- Ensure AJAX requests aren't blocked
- Verify cart endpoints are accessible

**Search not working:**
- Check search overlay HTML structure
- Verify search input IDs match JavaScript
- Ensure search API is enabled

**Mobile menu not opening:**
- Verify button IDs match JavaScript selectors
- Check for CSS conflicts
- Ensure click events aren't prevented

**Currency conversion issues:**
- Update exchange rates regularly
- Check geolocation API availability
- Verify country code mappings

### Debug Mode

Enable console logging by adding to theme.js:

```javascript
window.AURA_DEBUG = true;
```

## Development

### File Structure
- Keep JavaScript modular and focused
- Use ES6+ features where supported
- Implement proper error handling
- Follow Shopify theme development best practices

### Performance Tips
- Minimize DOM queries
- Use event delegation
- Implement debouncing for scroll/resize events
- Lazy load non-critical features

### Testing
- Test on multiple devices and browsers
- Verify cart functionality across different scenarios
- Test search with various query types
- Validate form submissions

## Browser Support

- Chrome 60+
- Firefox 55+
- Safari 12+
- Edge 79+
- Mobile browsers (iOS Safari, Chrome Mobile)

## License

This theme is proprietary software. Please refer to your license agreement for usage terms.

---

For additional support or customization requests, please contact the theme developer.
```

```markdown:API.md
# Aura Theme - API Documentation

## JavaScript Classes and Methods

### CartManager Class

#### Constructor
```javascript
new CartManager()
```
Initializes cart management functionality.

#### Methods

##### `init()`
Sets up event listeners and initializes the cart manager.

##### `bindEvents()`
Binds click and change events for cart interactions.

##### `handleQuantityChange(button)`
**Parameters:**
- `button` (HTMLElement) - The quantity button element

Handles increase/decrease quantity button clicks.

##### `handleInputChange(input)`
**Parameters:**
- `input` (HTMLElement) - The quantity input element

Handles direct quantity input changes.

##### `handleRemoveItem(link)`
**Parameters:**
- `link` (HTMLElement) - The remove item link

Handles item removal from cart.

##### `updateCart(itemId, quantity)`
**Parameters:**
- `itemId` (string) - The cart item ID
- `quantity` (number) - New quantity

Updates cart via Shopify Cart API.

### CartDrawer Class

#### Constructor
```javascript
new CartDrawer()
```
Initializes the cart drawer with multi-currency support.

#### Properties

##### `exchangeRates`
Object containing currency conversion rates and symbols.

##### `cart`
Current cart state object.

##### `isOpen`
Boolean indicating drawer state.

#### Methods

##### `init()`
Initializes drawer functionality and event listeners.

##### `detectUserCountry()`
**Returns:** Promise
Detects user's country for currency conversion.

##### `open()`
Opens the cart drawer with animation.

##### `close()`
Closes the cart drawer with animation.

##### `fetchCart()`
**Returns:** Promise
Fetches current cart data from Shopify.

### AddToCartManager Class

#### Constructor
```javascript
new AddToCartManager()
```
Manages add to cart and wishlist functionality.

#### Methods

##### `init()`
Initializes the add to cart system.

##### `bindEvents()`
Sets up event delegation for add to cart buttons.

##### `handleAddToCart(button)`
**Parameters:**
- `button` (HTMLElement) - Add to cart button

**Returns:** Promise
Handles adding products to cart.

##### `handleWishlist(button)`
**Parameters:**
- `button` (HTMLElement) - Wishlist button

Handles wishlist functionality.

##### `setButtonState(button, state)`
**Parameters:**
- `button` (HTMLElement) - Button element
- `state` (string) - State: 'loading', 'success', 'default'

Updates button visual state.

##### `updateCartCount()`
Updates cart count display in header.

##### `showNotification(message, type)`
**Parameters:**
- `message` (string) - Notification message
- `type` (string) - Type: 'success', 'error'

Shows user notification.

### Collection Filtering

#### Function: `collectionFiltering()`
**Returns:** Object with filtering functionality

#### Properties

##### `allProducts`
Array of all products in collection.

##### `filters`
Object containing active filters:
```javascript
{
  availability: [],
  color: [],
  size: []
}
```

##### `sortBy`
Current sort method.

#### Computed Properties

##### `hasActiveFilters`
**Returns:** Boolean
True if any filters are active.

##### `visibleProductCount`
**Returns:** Number
Count of currently visible products.

##### `availableColors`
**Returns:** Map
Available color options with hex codes.

#### Methods

##### `init()`
Initializes filtering system.

##### `loadProductData()`
Loads product data from DOM.

##### `applyFiltersAndSort()`
Applies current filters and sorting.

## Event System

### Custom Events

#### Cart Events
```javascript
// Cart updated
document.dispatchEvent(new CustomEvent('cart:updated', {
  detail: { cart: cartData }
}));

// Item added to cart
document.dispatchEvent(new CustomEvent('cart:item-added', {
  detail: { item: itemData }
}));
```

#### Search Events
```javascript
// Search performed
document.dispatchEvent(new CustomEvent('search:performed', {
  detail: { query: searchQuery, results: results }
}));
```

### Event Listeners

#### Global Click Handler
```javascript
document.addEventListener('click', (e) => {
  // Handles various button clicks through delegation
});
```

## Data Attributes

### Cart Elements
```html
<!-- Quantity buttons -->
<button data-action="increase" data-id="VARIANT_ID">+</button>
<button data-action="decrease" data-id="VARIANT_ID">-</button>

<!-- Add to cart -->
<button data-variant-id="VARIANT_ID" data-product-title="TITLE">
  Add to Cart
</button>

<!-- Wishlist -->
<button data-product-id="PRODUCT_ID">Add to Wishlist</button>
```

### Mobile Menu
```html
<!-- Submenu trigger -->
<button data-target="submenu-id">Open Submenu</button>

<!-- Back button -->
<button data-back="parent-menu-id">Back</button>
```

## Configuration Objects

### Currency Configuration
```javascript
const currencyConfig = {
  'COUNTRY_CODE': {
    currency: 'CURRENCY_CODE',
    rate: EXCHANGE_RATE,
    symbol: 'CURRENCY_SYMBOL'
  }
};
```

### Filter Configuration
```javascript
const filterConfig = {
  productsPerPage: 15,
  sortBy: 'manual',
  openFilters: {
    availability: true,
    color: true,
    size: true
  }
};
```

## Shopify Integration

### Liquid Variables Required

#### Product Data
```liquid
<script id="collection-products" type="application/json">
  {{ collection.products | json }}
</script>
```

#### Cart Data
```liquid
<script id="cart-data" type="application/json">
  {{ cart | json }}
</script>
```

### Required Shopify Sections
- `cart-drawer.liquid`
- `mobile-menu.liquid`
- `search-overlay.liquid`
- `product-card.liquid`

# Aura Theme - API Documentation (Continued)

## Error Handling

### Try-Catch Blocks
All AJAX operations include proper error handling:

```javascript
try {
  const response = await fetch('/cart/add.js', options);
  if (!response.ok) {
    throw new Error('Network response was not ok');
  }
  const data = await response.json();
  // Handle success
} catch (error) {
  console.error('Cart operation failed:', error);
  // Handle error state
}
```

### Error Types

#### Cart Errors
- `VARIANT_NOT_FOUND` - Invalid variant ID
- `OUT_OF_STOCK` - Product unavailable
- `NETWORK_ERROR` - Connection issues

#### Search Errors
- `SEARCH_TIMEOUT` - Search request timeout
- `INVALID_QUERY` - Malformed search query

#### Form Errors
- `VALIDATION_ERROR` - Form validation failed
- `SUBMISSION_ERROR` - Form submission failed

## Utility Functions

### Currency Conversion
```javascript
convertPrice(price, fromCurrency, toCurrency) {
  const rate = this.exchangeRates[toCurrency]?.rate || 1;
  return (price * rate).toFixed(2);
}
```

### Debounce Function
```javascript
function debounce(func, wait) {
  let timeout;
  return function executedFunction(...args) {
    const later = () => {
      clearTimeout(timeout);
      func(...args);
    };
    clearTimeout(timeout);
    timeout = setTimeout(later, wait);
  };
}
```

### Animation Helpers
```javascript
// Slide animations
function slideIn(element) {
  element.classList.remove('hidden', '-translate-x-full');
  element.classList.add('translate-x-0');
}

function slideOut(element) {
  element.classList.add('-translate-x-full');
  element.classList.remove('translate-x-0');
}
```

## Performance Optimization

### Lazy Loading
```javascript
// Intersection Observer for lazy loading
const observer = new IntersectionObserver((entries) => {
  entries.forEach(entry => {
    if (entry.isIntersecting) {
      // Load content
      observer.unobserve(entry.target);
    }
  });
});
```

### Request Batching
```javascript
// Batch multiple cart updates
const batchCartUpdates = (updates) => {
  return fetch('/cart/update.js', {
    method: 'POST',
    headers: { 'Content-Type': 'application/json' },
    body: JSON.stringify({ updates })
  });
};
```

## Testing Utilities

### Mock Functions
```javascript
// Mock cart API for testing
window.mockCartAPI = {
  add: (items) => Promise.resolve({ items }),
  update: (updates) => Promise.resolve({ success: true }),
  get: () => Promise.resolve({ items: [], total_price: 0 })
};
```

### Debug Helpers
```javascript
// Enable debug mode
window.AURA_DEBUG = true;

// Debug logger
function debugLog(message, data) {
  if (window.AURA_DEBUG) {
    console.log(`[AURA] ${message}`, data);
  }
}
```

## Browser Compatibility

### Polyfills Required
- `fetch()` for older browsers
- `Promise` for IE11
- `IntersectionObserver` for older Safari

### Feature Detection
```javascript
// Check for required features
const hasRequiredFeatures = () => {
  return (
    'fetch' in window &&
    'Promise' in window &&
    'addEventListener' in document
  );
};
```

## Security Considerations

### CSRF Protection
```javascript
// Include CSRF token in requests
const csrfToken = document.querySelector('meta[name="csrf-token"]')?.content;

fetch('/cart/add.js', {
  headers: {
    'X-CSRF-Token': csrfToken,
    'Content-Type': 'application/json'
  }
});
```

### Input Sanitization
```javascript
// Sanitize user input
function sanitizeInput(input) {
  return input.replace(/<script\b[^<]*(?:(?!<\/script>)<[^<]*)*<\/script>/gi, '');
}
```

## Migration Guide

### From Previous Versions

#### v1.0 to v2.0
1. Update cart drawer HTML structure
2. Replace old event listeners with new delegation system
3. Update currency configuration format

#### Breaking Changes
- `CartManager.addToCart()` now returns Promise
- Filter configuration object structure changed
- Mobile menu data attributes updated

## Hooks and Filters

### Before Cart Add
```javascript
document.addEventListener('cart:before-add', (e) => {
  // Modify item before adding
  e.detail.item.properties = { custom: 'value' };
});
```

### After Search
```javascript
document.addEventListener('search:complete', (e) => {
  // Process search results
  console.log('Search results:', e.detail.results);
});
```

## Extending the Theme

### Adding Custom Modules
```javascript
// Create new module
class CustomModule {
  constructor() {
    this.init();
  }
  
  init() {
    // Module initialization
  }
}

// Initialize after DOM ready
document.addEventListener('DOMContentLoaded', () => {
  new CustomModule();
});
```

### Plugin Architecture
```javascript
// Register plugin
window.AuraPlugins = window.AuraPlugins || [];
window.AuraPlugins.push({
  name: 'CustomPlugin',
  init: function() {
    // Plugin code
  }
});
```

---

This completes the comprehensive API documentation for the Aura Shopify theme.
```

Now let me create a quick setup guide:

```markdown:SETUP.md
# Aura Theme - Quick Setup Guide

## Prerequisites
- Shopify store with theme development access
- Basic knowledge of Liquid templating
- Understanding of JavaScript and CSS

## Installation Steps

### 1. Theme Upload
1. Download theme files
2. Go to Shopify Admin → Online Store → Themes
3. Click "Upload theme" and select the theme zip file
4. Click "Publish" to make it live

### 2. Required Liquid Templates
Ensure these templates exist in your theme:

```liquid
<!-- templates/cart.liquid -->
<div id="cart-page">
  <!-- Cart content -->
</div>

<!-- sections/cart-drawer.liquid -->
<div id="cart-drawer-overlay" class="hidden">
  <div id="cart-drawer">
    <!-- Drawer content -->
  </div>
</div>

<!-- sections/mobile-menu.liquid -->
<div id="mobileMenu" class="hidden">
  <!-- Mobile menu content -->
</div>

<!-- sections/search-overlay.liquid -->
<div id="searchOverlay" class="hidden">
  <input id="searchInput" type="text">
  <div id="searchSuggestions"></div>
</div>
```

### 3. JavaScript Initialization
Add to your theme.liquid layout:

```liquid
<!-- Before closing </body> tag -->
<script>
  // Initialize theme modules
  document.addEventListener('DOMContentLoaded', function() {
    // Cart functionality
    if (typeof CartManager !== 'undefined') {
      window.cartManager = new CartManager();
    }
    
    // Cart drawer
    if (typeof CartDrawer !== 'undefined') {
      window.cartDrawer = new CartDrawer();
    }
    
    // Add to cart system
    if (typeof AddToCartManager !== 'undefined') {
      window.addToCartManager = new AddToCartManager();
    }
  });
</script>
```

### 4. CSS Classes Required
Add these CSS classes to your stylesheet:

```css
/* Loading states */
.loading { opacity: 0.6; pointer-events: none; }
.hidden { display: none; }

/* Animations */
.fade-in { opacity: 1; transition: opacity 0.3s ease; }
.fade-in-on-scroll { opacity: 0; transition: opacity 0.5s ease; }

/* Cart drawer */
.cart-drawer-overlay { 
  position: fixed; 
  top: 0; 
  left: 0; 
  width: 100%; 
  height: 100%; 
  background: rgba(0,0,0,0.5); 
  z-index: 1000; 
}

/* Mobile menu */
.mobile-menu { 
  transform: translateX(-100%); 
  transition: transform 0.3s ease; 
}
.mobile-menu.open { 
  transform: translateX(0); 
}

/* Search overlay */
.search-overlay { 
  transform: translateY(-100%); 
  transition: transform 0.3s ease; 
}
```

### 5. HTML Data Attributes
Update your product templates with required data attributes:

```liquid
<!-- Product cards -->
<div class="product-card">
  <button class="add-to-cart-btn" 
          data-variant-id="{{ product.selected_or_first_available_variant.id }}"
          data-product-title="{{ product.title | escape }}">
    Add to Cart
  </button>
  
  <button class="wishlist-btn" 
          data-product-id="{{ product.id }}">
    ♡
  </button>
</div>

<!-- Cart page -->
<tr id="item_{{ item.variant_id }}">
  <td>
    <button class="quantity-btn" 
            data-action="decrease" 
            data-id="{{ item.variant_id }}">-</button>
    <input class="quantity-input" 
           data-id="{{ item.variant_id }}" 
           value="{{ item.quantity }}">
    <button class="quantity-btn" 
            data-action="increase" 
            data-id="{{ item.variant_id }}">+</button>
  </td>
  <td>
    <a href="#" class="remove-items">Remove</a>
  </td>
</tr>
```

### 6. Collection Filtering Setup
For collection pages with filtering:

```liquid
<!-- Collection template -->
<script id="collection-products" type="application/json">
  {{ collection.products | json }}
</script>

<div x-data="collectionFiltering()" x-init="init()">
  <!-- Filter controls -->
  <div class="filters">
    <!-- Availability filter -->
    <div>
      <h3>Availability</h3>
      <label>
        <input type="checkbox" x-model="filters.availability" value="in-stock">
        In Stock
      </label>
    </div>
    
    <!-- Color filter -->
    <div>
      <h3>Color</h3>
      <template x-for="color in availableColors">
        <label>
          <input type="checkbox" x-model="filters.color" :value="color.name">
          <span :style="`background-color: ${color.hex}`"></span>
          <span x-text="color.name"></span>
        </label>
      </template>
    </div>
  </div>
  
  <!-- Product grid -->
  <div class="product-grid">
    {% for product in collection.products %}
      <div class="product-item" 
           data-availability="{{ product.available }}"
           data-colors="{{ product.metafields.custom.colors | json }}"
           data-sizes="{{ product.metafields.custom.sizes | json }}">
        <!-- Product content -->
      </div>
    {% endfor %}
  </div>
</div>
```

### 7. Contact Form Setup
```liquid
<!-- Contact form -->
<form id="contact-form" action="/contact" method="post">
  <input type="text" name="contact[name]" required>
  <input type="email" name="contact[email]" required>
  <textarea name="contact[body]" required></textarea>
  
  <button type="submit" id="submit-btn">
    <span id="btn-text">Send Message</span>
    <span id="btn-loading" class="hidden">Sending...</span>
  </button>
</form>

<div id="form-messages"></div>
```

### 8. Testing Checklist
- [ ] Cart add/remove functionality works
- [ ] Cart drawer opens and closes
- [ ] Mobile menu navigation works
- [ ] Search overlay functions properly
- [ ] Collection filtering works
- [ ] Contact form submits successfully
- [ ] Multi-currency conversion (if enabled)
- [ ] Responsive design on mobile devices

### 9. Optional Configurations

#### Enable Debug Mode
```javascript
window.AURA_DEBUG = true;
```

#### Customize Currency Rates
Update rates in `cart-drawer.js`:
```javascript
exchangeRates: {
  'US': { currency: 'USD', rate: 1, symbol: '$' },
  'PK': { currency: 'PKR', rate: 280, symbol: 'Rs.' },
  // Add your currencies here
}
```

#### Modify Filter Settings
Update in `collection-filtering.js`:
```javascript
productsPerPage: 20, // Change products per page
sortBy: 'price-ascending', // Default sort
```

## Troubleshooting

### Common Issues
1. **Cart not updating**: Check variant IDs and AJAX endpoints
2. **Search not working**: Verify search overlay HTML structure
3. **Mobile menu not opening**: Check button IDs and event listeners
4. **Filters not working**: Ensure Alpine.js is loaded and data attributes are correct

### Support
For additional help, check the full documentation or contact theme support.
