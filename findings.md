# Findings

## Rendering

- Initial page render is significantly delay.
  - **Baseline**: LCP/FCP
  - **Cause**:
    - Main HTML is too large; optimized for HTTP/1.
    - 70kb icon map is inlined.
  - **Solution**:
    - Re-optimize HTML pages for HTTP/2. Do _not_ inline CSS+JS. Do _not_ bundle JS excessively.
    - make icon map external.

- Initial visual page load is significantly delayed.
  - **Baseline**: LCP/FCP
  - **Cause**:
    - First article image is loaded in parallel with every other image.
    - First article "image" is a video.
  - **Solution**:
    - Add `fetchpriority=high` to first article images.
    - Use an image for first-article, replace with video on click.

- Initial page functionality is significantly delayed.
  - **Cause**: Too many 3rd-party scripts, all inline.
  - **Solution**: Reduce 3rd-party scripts to necessary. Make lazy when possible. Bundle static.

- Images do not render in order of user need.
  - **Baseline**: Performance
  - **Causes**: Images lack priority indicators. Ad sometimes loads before headline story. Secondary always loads before headline story.
  - **Solution**: add `fetchpriority` to all images as appropriate.

- Delayed ad makes page look broken.
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
  - **Baseline**: Accessibility is only buttons and links without accessible names, images without alt.
  - **Cause**: Icon-only buttons/links have no text or aria-label, and several images ship without alt attributes; headings are also out of order.
  - **Solution**: Add aria-label to icon buttons and links, provide alt text on images, fix heading order, and add title to iframes.
