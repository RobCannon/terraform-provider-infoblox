
# Infoblox Provider

The Inflbox provider is used to interact with the
resources supported by Infoblox. The provider needs to be configured
with the proper credentials before it can be used.

Use the navigation to the left to read about the available resources.

## Example Usage

```
# Configure the Infoblox provider
provider "infoblox" {
    username = "${var.infoblox_username}"
    password = "${var.infoblox_password}"
    host  = "${var.infoblox_host}"
    sslverify = "${var.infoblox_sslverify}"
    usecookies = "${var.infoblox_usecookies}"
}

# Create a record
resource "infoblox_record" "www" {
    ...
}
```

## Argument Reference

The following arguments are supported:

* `username` - (Required) The Infoblox username. It must be provided, but it can also be sourced from the `INFOBLOX_USERNAME` environment variable.
* `password` - (Required) The password associated with the username. It must be provided, but it can also be sourced from the `INFOBLOX_PASSWORD` environment variable.
* `host` - (Required) The base url for the Infoblox REST API, but it can also be sourced from the `INFOBLOX_HOST` environment variable.
* `sslverify` - (Required) Enable ssl for the REST api, but it can also be sourced from the `INFOBLOX_SSLVERIFY` environment variable.
* `usecookies` - (Optional) Use cookies to connect to the REST API, but it can also be sourced from the `INFOBLOX_USECOOKIES` environment variable

# infoblox\_record

Provides a Infoblox record resource.

## Example Usage

```
# Add a record to the domain
resource "infoblox_record" "foobar" {
	value = "192.168.0.10"
	name = "terraform"
	domain = "mydomain.com"
	type = "A"
	ttl = 3600
}
```

## Argument Reference

See [related part of Infoblox Docs](https://godoc.org/github.com/fanatic/go-infoblox) for details about valid values.

The following arguments are supported:

* `domain` - (Required) The domain to add the record to
* `value` - (Required) The value of the record; its usage will depend on the `type` (see below)
* `name` - (Required) The name of the record
* `ttl` - (Integer, Optional) The TTL of the record
* `type` - (Required) The type of the record

## DNS Record Types

The type of record being created affects the interpretation of the `value` argument.

#### A Record

* `value` is the hostname

#### CNAME Record

* `value` is the alias name

#### AAAA Record

* `value` is the IPv6 address

## Attributes Reference

The following attributes are exported:

* `domain` - The domain of the record
* `value` - The value of the record
* `name` - The name of the record
* `type` - The type of the record
* `ttl` - The TTL of the record
