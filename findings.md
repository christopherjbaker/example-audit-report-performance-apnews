# Findings

- Visible page load is significantly delayed.
  - **Metric**: LCP is too big.
  - **Cause**: First article image is loaded in parallel with every other image.
  - **Solution**: Add `fetchpriority=high` to first article images, add `fetchpriority=low` to 3+ article images.
