# Surge Config (CN)

An original Surge 6 configuration for users who want Chinese-language service groups, region-based node groups, encrypted DNS defaults, and a single proxy group that can control all service groups.

This project is a community configuration, not an official Surge project. Surge is a commercial product; a valid Surge license is required.

## Features

- Service groups for Telegram, Netflix, Disney+, YouTube, Bilibili, global media, AI services, Apple, Microsoft, and games.
- Every service group includes `✈️ 节点选择`, so changing the main node group can control service traffic uniformly. Region choices and selected `DIRECT` choices remain available where relevant.
- Region groups use `smart` selection over the user's subscription nodes. Node names must contain a recognized country flag or region keyword; edit the filters if your provider uses different names.
- DoH is configured for ordinary DNS lookups. Traditional DNS on port 53 is hijacked when Surge VIF / Enhanced Mode handles the traffic.
- MITM is not configured or enabled by default.
- Personal rules and host mappings are kept out of the shared base configuration.

## Install

1. Download `Surge-CN.conf` and open it with Surge 6 on macOS or iOS.
2. Replace the example subscription URL in the `🚀 我的节点` policy group with your own Surge-compatible subscription URL.
3. Check the region regex filters against your provider's node names. Nodes with unrecognized names will remain available in `🚀 我的节点` but won't appear in a region group.
4. Enable Surge VIF / Enhanced Mode if you expect Surge to intercept hard-coded DNS requests and cover traffic outside the system proxy. `hijack-dns` only handles traditional port 53 DNS; it cannot block app-specific DoH/DoT or traffic that bypasses Surge.
5. Test DNS and routing after installation. DNS availability varies by ISP and region; replace the configured DoH providers if they return empty answers or are unreachable on your network.

The example subscription URL uses the reserved `.invalid` domain and will not work until you replace it.

## DNS and privacy notes

`encrypted-dns-server` sends ordinary DNS lookups to the configured DoH resolvers. `dns-server` supplies bootstrap resolvers used for connectivity checks and resolving encrypted DNS endpoint hostnames. The configured resolvers learn the names they resolve. Choose providers you trust and whose service is reachable from your network.

`hijack-dns = *:53` intercepts traditional DNS packets on port 53 when Surge VIF is active. It is not a universal DNS leak guarantee: apps can use their own encrypted DNS, and traffic can bypass the tunnel. Do not describe DNS interception as preventing every form of DNS disclosure.

## Personal overrides

`Custom.conf.example` is a blank template for personal domain rules and local host mappings. Copy only the entries you need into the corresponding sections of your private profile. Do not put personal domains, subscription URLs, credentials, or private IP mappings in a public fork unless you intend to disclose them.

## Optional MITM / Sub-Store

MITM is intentionally absent from the default profile. Only enable it if a feature you choose (for example, a Sub-Store workflow that requires HTTPS interception) explicitly needs it. Follow that feature's current documentation, install and trust the Surge CA only on devices you control, and restrict the MITM hostname list to the minimum required domains. Keep certificate verification enabled; do not use `skip-server-cert-verify = true` as a workaround. Remove the CA from devices when you no longer need interception.

## Upstream rules and acknowledgements

The configuration structure and service-category choices were informed by publicly shared Surge configurations, including [Rabbit-Spec/Surge](https://github.com/Rabbit-Spec/Surge). This repository does not copy its configuration text. Rule lists are fetched from their upstream project at runtime and remain subject to each upstream project's terms and availability. Review those sources before relying on them.

## License

Original files in this repository are provided under the MIT License. This license does not apply to Surge itself, external rule lists, linked projects, or other third-party material. See [LICENSE](LICENSE).
