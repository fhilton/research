# WebDev

## Test Domains locally with Rider
Useful for testing UrlRewrite or subdomains.

### Setup domain to point to local IIS Express
- Modify C:\Windows\System32\drivers\etc\hosts to point the url to localhost
``` 
127..0.1 testdomian.com
```
- In Rider
  - Edit the Run/Debug configuration
    - Right click on web project and select properties->Web
    - Uncheck "Generate applicationhost.config"
      - This keeps your changes from being overwritten
    - Click on "Open applicationhost.config" link
    - Add a new binding for testdomain.com
``` xml
<sites>
     ...
      <site name="YourSite" id="1">
        ...
        <bindings>
          <binding protocol="http" bindingInformation="*:5000:localhost" />
          <binding protocol="https" bindingInformation="*:44300:localhost" />
          <binding protocol="https" bindingInformation="*:44300:testdomain.com" />
        </bindings>
      </site>
</sites>
```
- Open Rider as Administrator so that the new domain can be registered in IIS Express
  - Otherwise get error: failed to register URL "https://testdomain.com:44300/" for site "YourSite" application "/". Error description: Access is denied. (0x80070005)
  - Note: Would be nice to not have to do this, look into it.
- Debug the app
  - Should see in console: Successfully registered URL "https://testdomain.com:44300/" for site "YourSite" application "/"

### Update rewrite rules in web.config and test against urls.
