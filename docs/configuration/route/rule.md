---
icon: material/new-box
---

!!! quote "Changes in sing-box 1.11.0"

    :material-plus: [action](#action)  
    :material-alert: [outbound](#outbound)  
    :material-plus: [network_type](#network_type)  
    :material-plus: [network_is_expensive](#network_is_expensive)  
    :material-plus: [network_is_constrained](#network_is_constrained)

!!! quote "Changes in sing-box 1.10.0"

    :material-plus: [client](#client)  
    :material-delete-clock: [rule_set_ipcidr_match_source](#rule_set_ipcidr_match_source)  
    :material-plus: [rule_set_ip_cidr_match_source](#rule_set_ip_cidr_match_source)  
    :material-plus: [process_path_regex](#process_path_regex)

!!! quote "Changes in sing-box 1.8.0"

    :material-plus: [rule_set](#rule_set)  
    :material-plus: [rule_set_ipcidr_match_source](#rule_set_ipcidr_match_source)  
    :material-plus: [source_ip_is_private](#source_ip_is_private)  
    :material-plus: [ip_is_private](#ip_is_private)  
    :material-delete-clock: [source_geoip](#source_geoip)  
    :material-delete-clock: [geoip](#geoip)  
    :material-delete-clock: [geosite](#geosite)

### Structure

```json
{
  "route": {
    "rules": [
      {
        "inbound": [
          "mixed-in"
        ],
        "ip_version": 6,
        "network": [
          "tcp"
        ],
        "auth_user": [
          "usera",
          "userb"
        ],
        "protocol": [
          "tls",
          "http",
          "quic"
        ],
        "client": [
          "chromium",
          "safari",
          "firefox",
          "quic-go"
        ],
        "domain": [
          "test.com"
        ],
        "domain_suffix": [
          ".cn"
        ],
        "domain_keyword": [
          "test"
        ],
        "domain_regex": [
          "^stun\\..+"
        ],
        "geosite": [
          "cn"
        ],
        "source_geoip": [
          "private"
        ],
        "geoip": [
          "cn"
        ],
        "source_ip_cidr": [
          "10.0.0.0/24",
          "192.168.0.1"
        ],
        "source_ip_is_private": false,
        "ip_cidr": [
          "10.0.0.0/24",
          "192.168.0.1"
        ],
        "ip_is_private": false,
        "source_port": [
          12345
        ],
        "source_port_range": [
          "1000:2000",
          ":3000",
          "4000:"
        ],
        "port": [
          80,
          443
        ],
        "port_range": [
          "1000:2000",
          ":3000",
          "4000:"
        ],
        "process_name": [
          "curl"
        ],
        "process_path": [
          "/usr/bin/curl"
        ],
        "process_path_regex": [
          "^/usr/bin/.+"
        ],
        "package_name": [
          "com.termux"
        ],
        "user": [
          "sekai"
        ],
        "user_id": [
          1000
        ],
        "clash_mode": [
          "direct"
        ],
        "network_type": [
          "wifi"
        ],
        "network_is_expensive": false,
        "network_is_constrained": false,
        "wifi_ssid": [
          "My WIFI"
        ],
        "wifi_bssid": [
          "00:00:00:00:00:00"
        ],
        "rule_set": [
          "geoip-cn",
          "geosite-cn"
        ],
        // deprecated
        "rule_set_ipcidr_match_source": false,
        "rule_set_ip_cidr_match_source": false,
        "invert": false,
        "action": "route",
        "outbound": "direct"
      },
      {
        "type": "logical",
        "mode": "and",
        "rules": [],
        "invert": false,
        "action": "route",
        "outbound": "direct"
      }
    ]
  }
}

```

!!! note ""

    You can ignore the JSON Array [] tag when the content is only one item

### Default Fields

!!! note ""

    The default rule uses the following matching logic:  
    (`domain` || `domain_suffix` || `domain_keyword` || `domain_regex` || `geosite` || `geoip` || `ip_cidr` || `ip_is_private`) &&  
    (`port` || `port_range`) &&  
    (`source_geoip` || `source_ip_cidr` || `source_ip_is_private`) &&  
    (`source_port` || `source_port_range`) &&  
    `other fields`

    Additionally, included rule-sets can be considered merged rather than as a single rule sub-item.

#### inbound

Tags of [Inbound](/configuration/inbound/).

#### ip_version

4 or 6.

Not limited if empty.

#### auth_user

Username, see each inbound for details.

#### protocol

Sniffed protocol, see [Protocol Sniff](/configuration/route/sniff/) for details.

#### client

!!! question "Since sing-box 1.10.0"

Sniffed client type, see [Protocol Sniff](/configuration/route/sniff/) for details.

#### network

`tcp` or `udp`.

#### domain

Match full domain.

#### domain_suffix

Match domain suffix.

#### domain_keyword

Match domain using keyword.

#### domain_regex

Match domain using regular expression.

#### geosite

!!! failure "Deprecated in sing-box 1.8.0"

    Geosite is deprecated and will be removed in sing-box 1.12.0, check [Migration](/migration/#migrate-geosite-to-rule-sets).

Match geosite.

#### source_geoip

!!! failure "Deprecated in sing-box 1.8.0"

    GeoIP is deprecated and will be removed in sing-box 1.12.0, check [Migration](/migration/#migrate-geoip-to-rule-sets).

Match source geoip.

#### geoip

!!! failure "Deprecated in sing-box 1.8.0"

    GeoIP is deprecated and will be removed in sing-box 1.12.0, check [Migration](/migration/#migrate-geoip-to-rule-sets).

Match geoip.

#### source_ip_cidr

Match source IP CIDR.

#### ip_is_private

!!! question "Since sing-box 1.8.0"

Match non-public IP.

#### ip_cidr

Match IP CIDR.

#### source_ip_is_private

!!! question "Since sing-box 1.8.0"

Match non-public source IP.

#### source_port

Match source port.

#### source_port_range

Match source port range.

#### port

Match port.

#### port_range

Match port range.

#### process_name

!!! quote ""

    Only supported on Linux, Windows, and macOS.

Match process name.

#### process_path

!!! quote ""

    Only supported on Linux, Windows, and macOS.

Match process path.

#### process_path_regex

!!! question "Since sing-box 1.10.0"

!!! quote ""

    Only supported on Linux, Windows, and macOS.

Match process path using regular expression.

#### package_name

Match android package name.

#### user

!!! quote ""

    Only supported on Linux.

Match user name.

#### user_id

!!! quote ""

    Only supported on Linux.

Match user id.

#### clash_mode

Match Clash mode.

#### network_type

!!! question "Since sing-box 1.11.0"

!!! quote ""

    Only supported in graphical clients on Android and Apple platforms.

Match network type.

Available values: `wifi`, `cellular`, `ethernet` and `other`.

#### network_is_expensive

!!! question "Since sing-box 1.11.0"

!!! quote ""

    Only supported in graphical clients on Android and Apple platforms.

Match if network is considered Metered (on Android) or considered expensive,
such as Cellular or a Personal Hotspot (on Apple platforms).

#### network_is_constrained

!!! question "Since sing-box 1.11.0"

!!! quote ""

    Only supported in graphical clients on Apple platforms.

Match if network is in Low Data Mode.

#### wifi_ssid

!!! quote ""

    Only supported in graphical clients on Android and Apple platforms.

Match WiFi SSID.

#### wifi_bssid

!!! quote ""

    Only supported in graphical clients on Android and Apple platforms.

Match WiFi BSSID.

#### rule_set

!!! question "Since sing-box 1.8.0"

Match [rule-set](/configuration/route/#rule_set).

#### rule_set_ipcidr_match_source

!!! question "Since sing-box 1.8.0"

!!! failure "Deprecated in sing-box 1.10.0"

    `rule_set_ipcidr_match_source` is renamed to `rule_set_ip_cidr_match_source` and will be remove in sing-box 1.11.0.

Make `ip_cidr` in rule-sets match the source IP.

#### rule_set_ip_cidr_match_source

!!! question "Since sing-box 1.10.0"

Make `ip_cidr` in rule-sets match the source IP.

#### invert

Invert match result.

#### action

==Required==

See [Rule Actions](../rule_action/) for details.

#### outbound

!!! failure "Deprecated in sing-box 1.11.0"

    Moved to [Rule Action](../rule_action#route).

### Logical Fields

#### type

`logical`

#### mode

==Required==

`and` or `or`

#### rules

==Required==

Included rules.
