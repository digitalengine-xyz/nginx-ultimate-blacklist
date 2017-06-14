# Nginx Ultimate Blacklist
**This was inspired by [oohnoitz/nginx-blacklist](https://github.com/oohnoitz/nginx-blacklist) and this awesome [PP article](https://perishablepress.com/4g-ultimate-user-agent-blacklist/), it extends the list to include a ridicuilious amounts of evil bots. Always defend your nginx!!**

**blacklist.conf** utilizes the following two nginx modules to achieve the same results as the original **bad-bot-blocker**: `ngx_http_geo_module` and `ngx_http_map_module`. This provides admins with a single configuration file used for blacklisting any bots or malicious web crawlers without the need to complicate server blocks.

----
## NGINX INSTALL
### Install
1. Save `blacklist.conf` somewhere accessible by nginx.
2. Include `blacklist.conf` in your `nginx.conf` before your server blocks.
3. Add the following in each server block you wish to apply the blacklist to:
    ```
    if ($bad_client) {
      return 403;
    }
    ```

### Configure

#### geo $validate_agent block
This contains the list of **IP Addresses** that should be allowed to use any **User-Agent** blocked. By default, it will block all IP addresses using any of the matching IP addresses.

Syntax:
```
  127.0.0.1                      0; 
```
Note: `0` = allow and `1` = deny.


#### geo $validate_client block
This contains the list of **IP Addresses** that should be blocked from accessing the site. This is used to check all IP addresses that don't match any of the offending User-Agent listed. By default, it will allow all IP addresses to do not match any current rules to access the site.

Syntax:
```
  127.0.0.1                      1;
```
Note: `0` = allow and `1` = deny.

## APACHE INSTALL
Just in case you are on the Apache platform, use the htAccess.txt file as the example for your implementation. Make sure to add the code to your .htAccess file.

### Goodluck and happy safe coding!!
