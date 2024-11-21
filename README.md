## CKAN Helm Chart

This is a fork of the [CKAN Helm Chart](https://github.com/ckan/ckan-helm) with some modifications to support Tapis OAuth.

### Manage users

To manage users, you can use the [CKAN API](https://docs.ckan.org/en/2.9/api/index.html).

```bash
ckan -c production.ini sysadmin add john_doe
```
