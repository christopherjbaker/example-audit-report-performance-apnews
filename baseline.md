# Baseline

## Core Web Vitals

- **Largest Contentful Paint (LCP)**: 2.9 s
- **Interaction to Next Paint (INP)**: 177 ms
- **Cumulative Layout Shift (CLS)**: 0.06

## PageSpeed Insights at `/`

- **Performance**: 37
- **Accessibility**: 75
- **Best Practices**: 77
- **SEO**: 85

- **First Contentful Paint** 7.0 s
- **Largest Contentful Paint** 26.7 s
- **Total Blocking Time** 750 ms
- **Cumulative Layout Shift** 0
- **Speed Index** 13.7 s

## Network Activity

- http/2
- 151 requests
- 15.7mb resources
- js/css: 267kb
- assets: 7564kb

- good compression
  - fresh: 9.9mb transfered (37% reduction)
  - all text files compressed with br/gzip
  - binary files not compressed

- very good caching on all local files
  - fresh: 9.9mb transfered
  - refresh immediate: 967kb transfered (90% reduction)
  - refresh 1d:
