# Project structure

Analytics được implement trên cả 3 project hiện tại của PageFly

* pfcore:
  * helpers/analytics: Xử lý live view tracking, folder này được build theo config của webpack
  * views/analytic: Show các analytics metrics
  * views/settings/analytics: Configs analytics on/off, timezone, session timeout
  * config/proxySetup.js: Setup proxy
  * sw\_cache.js: Sử dụng service-worker để cache analytics requests&#x20;
* pfserver:
  * routers/analytics: api version 1
  * routers/analytics-v2: api version 2
  * helpers/analytics
* pf-analytic-server:
  * collect data endpoint
  * kết nối analytics database
  * Tính toán các metrics dựa trên tracking data
