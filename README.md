# Grafana dashboards

Find exported dashboards for Grafana that can be useful when troubleshooting platform issues.

By default Healthwatch 2 (Grafana) uses prometheus as its default and only data source.
While not officially supported for customers, you can add the Metric store as a data source. Here are the steps:
 
1. Utilizing the UAA-based RBAC for Metric Store, which controls access to metrics based upon what spaces a user has access to
  a. Set up Healthwatch with UAA integration for Grafana. Docs to do so are here: https://docs.pivotal.io/healthwatch/2-1/configuring/grafana-authentication.html#configure-uaa but admittedly they need a little work. I'll be working to clean those up this week, but if you get stuck please reach out and we can help you.
  b. Create a datasource in Grafana for metric store using https://metric-store.service.internal:8083 as the URL.  Make sure to also select Forward OAuth Identity and HTTP Method GET
2. Utilizing mtls-based Admin access (recommended)
  a. This provides access to any metric in metric store, so the authentication type for Grafana itself doesn't matter
  b. Create a datasource in Grafana for metric store using https://metric-store.service.internal:8080 as the URL.
  c. Select TLS Client Auth and With CA Cert
  d. The CA cert should be the Ops Manager CA Cert
  e. The cert and key can be generated using om generate-certificate . The domain used doesn't matter
  f. Make sure to set ServerName to metric-store
  g. HTTP method = GET