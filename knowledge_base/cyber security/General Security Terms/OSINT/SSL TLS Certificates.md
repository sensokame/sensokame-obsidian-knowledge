# SSL/TLS Certificates
when an [[SSL]]/[[TLS]] certificate is created for a domain by a [[CA]], the [[CA]] keeps a Certificate Transparency log, these are publicly assessible logs. their purpose is to stop malicious and accidental certificates from being used (basically, the log shows which websites are actually given authentic [[CA]]s) we can use this service to discover subdomains belonging to a domain since they would most likely be given the same cert.
some of the websites used for doing this include
- [crt.sh](https://crt.sh)
- [ctseach](https://ui.ctsearch.entrust.com/ui/ctsearchui)
