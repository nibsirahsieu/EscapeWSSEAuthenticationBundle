## Introduction

The EscapeWSSEAuthentication bundle is a simple and easy way to implement WSSE authentication in Symfony2 applications

## Installation

deps

```
[EscapeWSSEAuthenticationBundle]
    git=https://github.com/escapestudios/EscapeWSSEAuthenticationBundle.git
    target=/bundles/Escape/EscapeWSSEAuthenticationBundle
    version=origin/2.0.x
```

app/autoload.php

```
$loader->registerNamespaces(array(
    //...
    'Escape' => __DIR__.'/../vendor/bundles',
    //...
  ));
```

app/AppKernel.php

```
public function registerBundles()
{
    return array(
        //...
        new Escape\WSSEAuthenticationBundle\EscapeWSSEAuthenticationBundle(),
        //...
    );
    ...
```

## Configuration

app/config/config.yml

```
# Escape WSSE authentication configuration
escape_wsse_authentication:
    provider_class: Escape\WSSEAuthenticationBundle\Security\Core\Authentication\Provider\Provider
    listener_class: Escape\WSSEAuthenticationBundle\Security\Http\Firewall\Listener
```

## Usage example

app/config/security.yml

nonce_dir: location where nonces will be saved (use null to skip nonce-validation)
lifetime: lifetime of nonce

```
firewalls:
    wsse_secured:
        pattern:   ^/api/.*
        wsse:      { nonce_dir: null, lifetime: 300 } 

factories:
    - "%kernel.root_dir%/../vendor/bundles/Escape/WSSEAuthenticationBundle/Resources/config/security_factories.yml"
```
