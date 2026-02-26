# Design Document

## Overview

This design implements tracking pixel ID "1444448173961324" across all HTML pages in the website. The solution adds a new Facebook Pixel alongside the existing pixel (4179716432354886) while maintaining all current functionality and following the same implementation patterns.

## Architecture

### Current State Analysis

The website currently implements Facebook Pixel tracking with the following structure:

```javascript
<!-- Facebook Pixel Code -->
<script>
  !function (f, b, e, v, n, t, s) {
    if (f.fbq) return; n = f.fbq = function () {
      n.callMethod ?
        n.callMethod.apply(n, arguments) : n.queue.push(arguments)
    };
    if (!f._fbq) f._fbq = n; n.push = n; n.loaded = !0; n.version = '2.0';
    n.queue = []; t = b.createElement(e); t.async = !0;
    t.src = v; s = b.getElementsByTagName(e)[0];
    s.parentNode.insertBefore(t, s)
  }(window, document, 'script',
    'https://connect.facebook.net/en_US/fbevents.js');

  fbq('init', '4179716432354886');
  fbq('track', 'PageView');
  // Additional events on specific pages
</script>
<!-- End Facebook Pixel Code -->
```

### Target Architecture

The new implementation will add a second pixel initialization while reusing the same Facebook Pixel infrastructure:

```javascript
<!-- Facebook Pixel Code -->
<script>
  !function (f, b, e, v, n, t, s) {
    if (f.fbq) return; n = f.fbq = function () {
      n.callMethod ?
        n.callMethod.apply(n, arguments) : n.queue.push(arguments)
    };
    if (!f._fbq) f._fbq = n; n.push = n; n.loaded = !0; n.version = '2.0';
    n.queue = []; t = b.createElement(e); t.async = !0;
    t.src = v; s = b.getElementsByTagName(e)[0];
    s.parentNode.insertBefore(t, s)
  }(window, document, 'script',
    'https://connect.facebook.net/en_US/fbevents.js');

  // Existing pixel
  fbq('init', '4179716432354886');
  fbq('track', 'PageView');
  
  // New pixel
  fbq('init', '1444448173961324');
  fbq('track', 'PageView');
  
  // Additional events on specific pages
</script>
<!-- End Facebook Pixel Code -->
```

## Implementation Strategy

### Approach: Direct Code Modification

**Rationale:** Given the small number of HTML files and the need for immediate implementation, direct modification of each HTML file is the most straightforward approach.

**Benefits:**
- Simple and direct implementation
- No additional infrastructure needed
- Follows existing patterns exactly
- Easy to verify and test

**Files to Modify:**
Based on the workspace analysis, the following HTML files need modification:
- `index.html`
- `checkout.html` 
- `delivery.html`
- `checkout-iphone.html`
- `checkout-micro.html`
- `checkout2.html`
- `delivery-iphone.html`
- `delivery-micro.html`
- `delivery2.html`
- `index2.html`
- `iphone17pro.html`
- `presell-iphone.html`
- `takemicro.html`

### Code Modification Pattern

For each HTML file, the modification will:

1. **Locate** the existing Facebook Pixel code block
2. **Add** the new pixel initialization after the existing one
3. **Maintain** all existing functionality and events
4. **Preserve** code formatting and structure

### Specific Implementation Details

#### Standard Pages (index.html, checkout.html, delivery.html, etc.)

Add these two lines after the existing `fbq('track', 'PageView');`:

```javascript
// New pixel
fbq('init', '1444448173961324');
fbq('track', 'PageView');
```

#### Pages with Additional Events

Some pages have additional tracking events (like ViewContent). The new pixel will track the same events:

```javascript
// Existing pixel
fbq('init', '4179716432354886');
fbq('track', 'PageView');
fbq('track', 'ViewContent'); // if present

// New pixel  
fbq('init', '1444448173961324');
fbq('track', 'PageView');
fbq('track', 'ViewContent'); // mirror the same events
```

## Technical Specifications

### Performance Considerations

- **Async Loading:** The Facebook Pixel library loads asynchronously, so adding a second pixel initialization has minimal performance impact
- **Single Library:** Both pixels use the same fbevents.js library, so no additional network requests
- **Event Batching:** Facebook Pixel automatically batches events, optimizing network usage

### Error Handling

- **Graceful Degradation:** If the Facebook Pixel library fails to load, both pixels will fail gracefully without breaking page functionality
- **Network Resilience:** The async loading pattern ensures page rendering is not blocked by tracking failures

### Browser Compatibility

- **Modern Browsers:** Full support in Chrome, Firefox, Safari, Edge
- **Legacy Support:** Facebook Pixel library handles browser compatibility automatically
- **JavaScript Disabled:** Pages function normally when JavaScript is disabled

## Correctness Properties

### Property 1: Dual Pixel Initialization
**Validates: Requirements 1.1, 1.2**

For any HTML page P in the website:
- WHEN P loads successfully
- THEN both pixel IDs ('4179716432354886' and '1444448173961324') SHALL be initialized
- AND both pixels SHALL fire PageView events

### Property 2: Event Mirroring
**Validates: Requirements 1.2, 2.2**

For any tracking event E on page P:
- WHEN the existing pixel fires event E
- THEN the new pixel SHALL also fire the same event E
- AND the event parameters SHALL be identical

### Property 3: Non-Interference
**Validates: Requirements 2.1, 2.3**

For the existing Facebook Pixel functionality:
- WHEN the new pixel is added to a page
- THEN all existing pixel events SHALL continue to fire normally
- AND existing pixel behavior SHALL remain unchanged

### Property 4: Implementation Consistency
**Validates: Requirements 6.1, 6.2, 6.3**

For all HTML pages in the website:
- WHEN comparing pixel implementation code
- THEN the code structure SHALL be identical across all pages
- AND the pixel placement SHALL be in the same location (head section)
- AND the initialization pattern SHALL follow the same format

## Testing Strategy

### Manual Testing Approach

1. **Browser Developer Tools:** Use Network tab to verify both pixels fire events
2. **Facebook Pixel Helper:** Browser extension to validate pixel implementation
3. **Page Load Testing:** Verify pages load normally with new pixel code
4. **Cross-Browser Testing:** Test in Chrome, Firefox, Safari, Edge

### Verification Steps

For each modified HTML file:
1. Open page in browser
2. Check browser console for JavaScript errors
3. Verify both pixel IDs appear in network requests
4. Confirm PageView events fire for both pixels
5. Test any page-specific events (ViewContent, etc.)

## Rollback Plan

If issues arise:
1. **Simple Revert:** Remove the two added lines from each HTML file
2. **Git Rollback:** Use version control to revert to previous state
3. **Selective Rollback:** Remove pixel from specific pages if needed

## Future Considerations

### Maintenance

- **New Pages:** When creating new HTML pages, include both pixel IDs
- **Event Updates:** When adding new tracking events, apply to both pixels
- **Pixel Management:** Consider centralizing pixel configuration in the future

### Scalability

- **Template System:** For future expansion, consider implementing a template-based approach
- **Configuration Management:** Centralized pixel ID configuration for easier updates
- **Automated Testing:** Implement automated pixel verification tests