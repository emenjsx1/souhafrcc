# Implementation Tasks

## Task Overview

This task list implements tracking pixel ID "1444448173961324" across all HTML pages by modifying the existing Facebook Pixel code blocks.

## Tasks

### 1. Core HTML Pages Implementation

- [ ] 1.1 Add new pixel to index.html
  - [ ] 1.1.1 Locate existing Facebook Pixel code block in index.html
  - [ ] 1.1.2 Add new pixel initialization after existing pixel
  - [ ] 1.1.3 Add PageView event for new pixel
  - [ ] 1.1.4 Add ViewContent event for new pixel (matches existing)
  - [ ] 1.1.5 Verify code formatting and structure

- [ ] 1.2 Add new pixel to checkout.html
  - [ ] 1.2.1 Locate existing Facebook Pixel code block in checkout.html
  - [ ] 1.2.2 Add new pixel initialization after existing pixel
  - [ ] 1.2.3 Add PageView event for new pixel
  - [ ] 1.2.4 Verify code formatting and structure

- [ ] 1.3 Add new pixel to delivery.html
  - [ ] 1.3.1 Locate existing Facebook Pixel code block in delivery.html
  - [ ] 1.3.2 Add new pixel initialization after existing pixel
  - [ ] 1.3.3 Add PageView event for new pixel
  - [ ] 1.3.4 Verify code formatting and structure

### 2. Variant Pages Implementation

- [ ] 2.1 Add new pixel to checkout-iphone.html
  - [ ] 2.1.1 Locate existing Facebook Pixel code block
  - [ ] 2.1.2 Add new pixel initialization and PageView event
  - [ ] 2.1.3 Verify implementation consistency

- [ ] 2.2 Add new pixel to checkout-micro.html
  - [ ] 2.2.1 Locate existing Facebook Pixel code block
  - [ ] 2.2.2 Add new pixel initialization and PageView event
  - [ ] 2.2.3 Verify implementation consistency

- [ ] 2.3 Add new pixel to checkout2.html
  - [ ] 2.3.1 Locate existing Facebook Pixel code block
  - [ ] 2.3.2 Add new pixel initialization and PageView event
  - [ ] 2.3.3 Verify implementation consistency

- [ ] 2.4 Add new pixel to delivery-iphone.html
  - [ ] 2.4.1 Locate existing Facebook Pixel code block
  - [ ] 2.4.2 Add new pixel initialization and PageView event
  - [ ] 2.4.3 Verify implementation consistency

- [ ] 2.5 Add new pixel to delivery-micro.html
  - [ ] 2.5.1 Locate existing Facebook Pixel code block
  - [ ] 2.5.2 Add new pixel initialization and PageView event
  - [ ] 2.5.3 Verify implementation consistency

- [ ] 2.6 Add new pixel to delivery2.html
  - [ ] 2.6.1 Locate existing Facebook Pixel code block
  - [ ] 2.6.2 Add new pixel initialization and PageView event
  - [ ] 2.6.3 Verify implementation consistency

### 3. Additional Pages Implementation

- [ ] 3.1 Add new pixel to index2.html
  - [ ] 3.1.1 Locate existing Facebook Pixel code block
  - [ ] 3.1.2 Add new pixel initialization and PageView event
  - [ ] 3.1.3 Verify implementation consistency

- [ ] 3.2 Add new pixel to iphone17pro.html
  - [ ] 3.2.1 Locate existing Facebook Pixel code block
  - [ ] 3.2.2 Add new pixel initialization and PageView event
  - [ ] 3.2.3 Verify implementation consistency

- [ ] 3.3 Add new pixel to presell-iphone.html
  - [ ] 3.3.1 Locate existing Facebook Pixel code block
  - [ ] 3.3.2 Add new pixel initialization and PageView event
  - [ ] 3.3.3 Verify implementation consistency

- [ ] 3.4 Add new pixel to takemicro.html
  - [ ] 3.4.1 Locate existing Facebook Pixel code block
  - [ ] 3.4.2 Add new pixel initialization and PageView event
  - [ ] 3.4.3 Verify implementation consistency

### 4. Testing and Verification

- [ ] 4.1 Browser Testing
  - [ ] 4.1.1 Test all pages in Chrome browser
  - [ ] 4.1.2 Test all pages in Firefox browser
  - [ ] 4.1.3 Test all pages in Safari browser
  - [ ] 4.1.4 Test all pages in Edge browser

- [ ] 4.2 Pixel Verification
  - [ ] 4.2.1 Use browser developer tools to verify both pixels fire on each page
  - [ ] 4.2.2 Install Facebook Pixel Helper extension and verify pixel detection
  - [ ] 4.2.3 Check network requests show both pixel IDs
  - [ ] 4.2.4 Verify PageView events fire for both pixels on all pages

- [ ] 4.3 Functionality Testing
  - [ ] 4.3.1 Verify all pages load without JavaScript errors
  - [ ] 4.3.2 Verify existing page functionality remains intact
  - [ ] 4.3.3 Test page interactions and form submissions work normally
  - [ ] 4.3.4 Verify page performance is not significantly impacted

### 5. Quality Assurance

- [ ] 5.1 Code Review
  - [ ] 5.1.1 Review all modified files for consistent implementation
  - [ ] 5.1.2 Verify pixel placement is identical across all pages
  - [ ] 5.1.3 Check code formatting and indentation consistency
  - [ ] 5.1.4 Ensure no existing code was accidentally modified

- [ ] 5.2 Documentation Update
  - [ ] 5.2.1 Document the new pixel ID in project documentation
  - [ ] 5.2.2 Update any developer guides with new pixel information
  - [ ] 5.2.3 Create maintenance notes for future pixel updates

### 6. Deployment Preparation

- [ ] 6.1 Pre-deployment Checklist
  - [ ] 6.1.1 Verify all HTML files have been modified
  - [ ] 6.1.2 Confirm no files were missed or incorrectly modified
  - [ ] 6.1.3 Test complete website functionality locally
  - [ ] 6.1.4 Prepare rollback plan documentation

- [ ] 6.2 Deployment Verification
  - [ ] 6.2.1 Deploy to staging environment and test
  - [ ] 6.2.2 Verify pixel tracking in staging environment
  - [ ] 6.2.3 Perform final cross-browser testing in staging
  - [ ] 6.2.4 Get approval for production deployment

## Implementation Notes

### Code Pattern to Add

For each HTML file, add these lines after the existing `fbq('init', '4179716432354886');` and `fbq('track', 'PageView');`:

```javascript
// New pixel
fbq('init', '1444448173961324');
fbq('track', 'PageView');
```

For pages with additional events (like ViewContent), mirror those events for the new pixel as well.

### Files to Modify

1. index.html
2. checkout.html
3. delivery.html
4. checkout-iphone.html
5. checkout-micro.html
6. checkout2.html
7. delivery-iphone.html
8. delivery-micro.html
9. delivery2.html
10. index2.html
11. iphone17pro.html
12. presell-iphone.html
13. takemicro.html

### Success Criteria

- All HTML pages load without errors
- Both pixel IDs (4179716432354886 and 1444448173961324) fire PageView events
- Existing functionality remains unchanged
- Implementation is consistent across all pages
- Cross-browser compatibility is maintained