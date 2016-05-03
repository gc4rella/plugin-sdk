OpenB aton Plugin SDK
----------------

Open Baton is an open source project providing a reference implementation of the NFVO and VNFM based on the [ETSI][NFV MANO] specification, is implemented in java using the [spring.io] framework. It consists of two main components: a NFVO and a generic VNFM. This project **plugin-sdk** contains modules that are needed to implement a plugin for Open Baton framework.

Please refer to our [documentation][vim-plugin] for more information about this project. Below there are just few details about the way you can use it.

#### How does this works? 

An Open Baton Plugin is a separate application that accepts requests from the NFVO to allocate and update resources on VIM. Plugin SDK provides an interface to develop the plugins to work with Openbaton NFVO or VNFM of your choice. SDK allows the communication through rabbitmq broker via AMQP messaging.

In order to create a VIM plugin for OpenBaton system you need to add to your gradle build file:

```gradle
buildscript {
    dependencies {
        classpath("org.springframework.boot:spring-boot-gradle-plugin:1.2.6.RELEASE")
    }
}

apply plugin: 'spring-boot'

project.ext{
	mainClass = 'path.to.the.StarterClass'
}

apply plugin: 'java'
apply plugin: 'maven'
repositories {
    mavenCentral()
    maven {
        url "http://193.175.132.176:8081/nexus/content/groups/public"
    }
}

dependencies {
    compile 'org.openbaton:plugin-sdk:2.0.0'
}
```

Than create a class that implement ClientInterfaces and the inherited methods.
Create another starter class and set the path to it in a variable mainClass.

the starter class can be like the following:

```java
import org.openbaton.plugin.PluginStarter;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class StarterClass {

    private static Logger log = LoggerFactory.getLogger(PluginStarter.class);

    public static void main(String[] args) {
        log.info("params are: pluginName registryIp registryPort\ndefault is openstack-plugin localhost 1099");

        PluginStartup.startPluginRecursive("./path-to-folder", true, "broker-ip", "5672", 15, "admin", "openbaton", "15672");
}
```

Then, compile & run it

### Development

Want to contribute? Great! Get in contact with us. You can find us on twitter @[openbaton]

### News and Website
Information about OpenBaton can be found on our website. Follow us on Twitter @[openbaton].

## License

Copyright (c) 2015-2016 Fraunhofer FOKUS. All rights reserved.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.


[nfvo-link]: https://github.com/openbaton/NFVO
[generic-link]:https://github.com/openbaton/generic-vnfm
[client-link]: https://github.com/openbaton/openbaton-client
[vim-plugin]: http://openbaton.github.io/documentation/vim-plugin/
[spring.io]:https://spring.io/
[NFV MANO]:http://docbox.etsi.org/ISG/NFV/Open/Published/gs_NFV-MAN001v010101p%20-%20Management%20and%20Orchestration.pdf
[openbaton]:http://twitter.com/openbaton
