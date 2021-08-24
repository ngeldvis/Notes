# How to Use ROS JavaScript Library in Nuxt Application

## Setup

```bash
# install roslibjs using npm
$ npm install roslib
```
```javascript
// plugins/ros.client.js

import { Ros } from 'roslib'
import Vuee from 'vue'

// Create ros global variable and inject it into the vue instance

const ros = Vue.observable(new Ros())

export default ({ app }, inject) => {
    inject('ros', ros)
}
```
```javascript
// nuxt.config.js

export default {
    // Make sure to add the plugin to the nuxt config file
    plugins: [
        '~/plugins/ros.client.js'
    ]
}
```

You can then access the global ros variable as `this.$ros` in any .vue file

## Connect to ROS

```html
<!-- Compopnent/Page.vue -->
<template>
    ...
</template>

<script>
export default {
    mounted: function() {
        this.connectToRos()
    },
    methods: {
        connectToRos() {
            this.isRosConnecting = true
            this.$ros.on('error', function (error) {
                this.rosError = error
                this.isRosConnecting = false
            })
            this.$ros.on('connection', function () {
                this.isRosConnected = true
                this.isRosConnecting = false
            })
            this.$ros.on('close', function () {
                this.isRosConnected = false
                this.isRosConnecting = false
            })
            this.$ros.connect('ws://localhost:PORT')
        }
    }
}
</script>
```

## Creating a Listener/Subscriber

```html
<!-- Component/Page.vue -->

<template>
    ...
</template>

<script>
import { Topic } from 'roslib'

export default {
    data() {
        return {
            topic: new Topic({
                ros: this.$ros,
                name: '/topic_name',
                messageType: 'message_type'
            })
        }
    },
    mouted: function() {
        this.subscribeToTopic()
    },
    methods: {
        subscribeToTopic() {
            this.topic.subscribe((message) => {
                // function that uses message
            })
        }
    }
}
</script>
```

## Creating a Publisher

```html
<script>
import { Message, Topic } from 'roslib'

export default {
    data() {
        return {
            topic: new Topic({
                ros: this.$ros,
                name: '/topic_name',
                messageType: 'message_type'
            })
        }
    },
    methods: {
        publish() {
            const message = new Message(data)
            this.topic.publish(message)
        }
    }
}
</script>
```
