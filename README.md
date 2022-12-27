# Country Relationships

These open source maps provide data on the relationships between countries, including friendships and potential conflicts. It is important to note that the data provided is based on official declarations from governments, as well as the current political situation and the author's own opinions. It is not intended to reflect the feelings or attitudes of the people in any particular country.

## Disclaimer
It is crucial to recognize that the relationships between countries can change over time and that it is not appropriate to use this data to make decisions about individuals or businesses from specific countries. Companies should ensure that they comply with all relevant laws and regulations, but it is not appropriate to rely on broad assumptions or stereotypes about entire countries or their citizens. It is always best to carefully research and consider the specific laws and regulations that apply to a particular situation.

## Use of Country Relationship Data

The data provided may be used by companies for the purpose of blocking or whitelisting requests from certain countries, in accordance with their own regulations related to doing business with other countries. However, it is important to note that these decisions should be made with care and should not be based on broad stereotypes or assumptions.

## TODO

### NGINX usage

Generated NGINX maps installed by `nginx-country-relationships` package at: `/etc/nginx/conf.d/country_relationships.conf`.
The content of this file looks like this:

```nginx
map $my_country:$geoip2_data_country_iso_code $country_conflicts {
    default 0;
    "RU:US" 1;
    "US:RU" 1;
    ...
}
```

To use the data for blocking a conflicting country, set your own country's two-letter ISO code, then add an `if` clause for an action,
that should be performed on the request.

```nginx
server {
    set my_country XX;
    if ($country_conflicts) {
        return 403;
    }
}
```    
