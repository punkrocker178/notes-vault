#material #swiperjs #migration
# Breaking changes from V14 to V16 (Current project): 
- Current Material components are now used as `LegacyComponent`
- Material theming conflicts with MDC components => Need to create a new theme to support both legacy and mdc components (`base-theme.config`)
- Swiper V9 removed Angular Swiper component 
- Material sass import errors on CI environment

In order to upgrade to V17, we need to migrate all `LegacyComponent` to MDC components