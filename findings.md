# Findings

## Rendering

- Initial page render is significantly delay.
  - **Prioritization**: 180.00
    - **Effort**: 2
    - **Reach**: 5
    - **Imact**:
      - **Initial Load**: 5
      - **Usability**: 3
      - **User Delight**: 1
  - **Baseline**: LCP/FCP
  - **Cause**:
    - Main HTML is too large; optimized for HTTP/1.
    - 70kb icon map is inlined.
  - **Solution**:
    - Re-optimize HTML pages for HTTP/2. Do _not_ inline CSS+JS. Do _not_ bundle JS excessively.
    - make icon map external.

- Initial visual page load is significantly delayed.
  - **Prioritization**: 147.50
    - **Effort**: 1
    - **Reach**: 5
    - **Imact**:
      - **Initial Load**: 5
      - **Usability**: 2
      - **User Delight**: 2
  - **Baseline**: LCP/FCP
  - **Cause**:
    - First article image is loaded in parallel with every other image.
    - First article "image" is a video.
  - **Solution**:
    - Add `fetchpriority=high` to first article images.
    - Use an image for first-article, replace with video on click.

- Initial page functionality is significantly delayed.
  - **Prioritization**: 95.00
    - **Effort**: 3
    - **Reach**: 4
    - **Imact**:
      - **Initial Load**: 3
      - **Usability**: 4
      - **User Delight**: 2
  - **Cause**: Too many 3rd-party scripts, all inline.
  - **Solution**: Reduce 3rd-party scripts to necessary. Make lazy when possible. Bundle static.

- Images do not render in order of user need.
  - **Prioritization**: 92.50
    - **Effort**: 1
    - **Reach**: 5
    - **Imact**:
      - **Initial Load**: 3
      - **Usability**: 2
      - **User Delight**: 2.5
  - **Baseline**: Performance
  - **Causes**: Images lack priority indicators. Ad sometimes loads before headline story. Secondary always loads before headline story.
  - **Solution**: add `fetchpriority` to all images as appropriate.

- Delayed ad makes page look broken.
  - **Prioritization**: 74.00
    - **Effort**: 2
    - **Reach**: 5
    - **Imact**:
      - **Initial Load**: 4
      - **Usability**: 3
      - **User Delight**: 2
  - **Baseline**: LCP/FCP
  - **Cause**: Ad is dynamic content. It renders after main image (good), but at the top of the page so page looks empty/broken until its ready.
  - **Solution**: Move ad below the fold or make it minor.
  - **TODO**: Create mock screenshot with ad moved down.

## Networking

### Good

- good compression
  - **Baseline**: network compression
  - 50%/60% reduction
  - all text files compressed with br/gzip
  - binary files not compressed

- good caching
  - **Baseline**: network caching
  - 88%/98% compression reduction
  - 99%/95% cache reduction

## Accessibility

- Interactive controls are invisible to assistive technology.
  - **Prioritization**: 50.67
    - **Effort**: 2
    - **Reach**: 2 -> 4
    - **Imact**:
      - **Initial Load**: 0
      - **Usability**: 5
      - **User Delight**: 4
  - **Baseline**: Accessibility is only buttons and links without accessible names, images without alt.
  - **Cause**: Icon-only buttons/links have no text or aria-label, and several images ship without alt attributes; headings are also out of order.
  - **Solution**: Add aria-label to icon buttons and links, provide alt text on images, fix heading order, and add title to iframes.
