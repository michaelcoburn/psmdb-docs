# FIPS compliance

FIPS (Federal Information Processing Standard) is the US government computer security standard for cryptography modules that include both hardware and software components. Percona Server for MongoDB supports FIPS certified module for OpenSSL, enabling US organizations to introduce FIPS-compliant encryption and thus meet the requirements towards data security.  

The FIPS compliance in Percona Server for MongoDB is implemented in the same way, as in MongoDB Enterprise. It is available in [Percona Server for MongoDB Pro out of the box](psmdb-pro.md) starting with version 7.0.4-2. You can also receive this functionality by [building Percona Server for MongoDB from source code](install/source.md).

See [Configure MongoDB for FIPS](https://www.mongodb.com/docs/v7.0/tutorial/configure-fips/) in MongoDB documentation for configuration guidelines. 