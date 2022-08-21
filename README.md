# Example Proxy - Envoy
A .NET example project on how to setup Envoy with a Web API service.

I wanted to learn how to setup Envoy for a project I was working on, but as someone who is not an expert on proxy servers and doesn't set them up often, I found it kinda tough to jump in and make it work the way I wanted.

This repo is a reference working setup with what I'd call the basics. It has a single ASP.NET Core Web API service, that has 2 separate instances configured, one for http and one for https. It shows you the Envoy configuration file to handle both http and https traffic from the outside, and route it to a cluster of services inside.

# Getting Started

You'll need the ASP.NET Core 6.0 SDK, and docker. For the TLS endpoint, you'll have to do some certificate work first. I documented my experience with that [here]().

You'll also need to copy the file src/.env.example to src/.env, and provide the password for the certificate you use for the service.

Once you get all that sorted, run this:
```
git clone https://github.com/hexsorcerer/example-proxy-envoy.git
cd example-proxy-envoy/src/
docker compose up -d
```

This command will run the system as 3 containers; Envoy, and 2 instances of Example.API. One instance is configured for TLS and one is not, but it is otherwise the same service.

You can connect to http://localhost:8080/WeatherForecast to hit the http version, or use https://localhost:8081/WeatherForecast to call the https version. They each behave the same, just showing the random weather JSON in the default web API project.