# Admin
Exposes the local administration interface.

In this example configuration, the listener address for this interface is restricted to 127.0.0.1 so that you must be connected to the machine in order to hit the admin endpoints.

See [admin operations](https://www.envoyproxy.io/docs/envoy/latest/operations/admin) in the official docs for more info.

# Static Resources
Envoy has two different kinds of resources, static and dynamic. Dynamic is discovery at runtime and is an advanced topic beyond the scope of this example.

See the [quickstart guide](https://www.envoyproxy.io/docs/envoy/latest/start/quick-start/configuration-static#start-quick-start-static-static-resources) and the [api reference](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/bootstrap/v3/bootstrap.proto#envoy-v3-api-msg-config-bootstrap-v3-bootstrap-staticresources) for more info.

# Listeners
Listeners are the public-facing ports where clients connect from the outside, and you can have multiple of these.

For more info see [listener configuration](https://www.envoyproxy.io/docs/envoy/latest/configuration/listeners/listeners#config-listeners) and the [api reference](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/listener/v3/listener.proto#envoy-v3-api-msg-config-listener-v3-listener) for more info.

# Filter Chains
Filter chains are sort of like middleware, they pass traffic from this listener through various filters and do various things with it. The most important filter is the http_connection_manager, which takes incoming traffic and routes it.

See [listener filters](https://www.envoyproxy.io/docs/envoy/latest/configuration/listeners/listener_filters/listener_filters) and the [api reference](https://www.envoyproxy.io/docs/envoy/latest/api-v3/config/listener/v3/listener_components.proto#envoy-v3-api-msg-config-listener-v3-filterchain) for more info.

# HTTP Connection Manager
A low-level filter that converts incoming bytes into http messages

See the [architecture overview](https://www.envoyproxy.io/docs/envoy/latest/intro/arch_overview/http/http_connection_management) and the [http_connection_manager configuration](https://www.envoyproxy.io/docs/envoy/latest/configuration/http/http_conn_man/http_conn_man#config-http-conn-man) for more info.

# Typed Configs
A typed config is essentially a unique identifier to the correct extension for this block of configuration, at least that was the best I could make of it.

See [extension configuration overview](https://www.envoyproxy.io/docs/envoy/latest/configuration/overview/extension) and [this stackoverflow answer](https://stackoverflow.com/a/63492368/8422356) for more info.

