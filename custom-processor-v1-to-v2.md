# Converting Custom Processor from V1 to V2

Converting a custom processor written for V1 to work in V2 is straightforward. Let's compare the the Mixpanel processor written for the request processing documentation in [V1](request-processing.md) and [V2](request-processing-v2.md):

1. Mixpanel Processor V1
```javascript
(function() {
    try {
        window.diver.processors.mixpanel = {
            name: 'Mixpanel',
            namespace: 'mixpanel',
            process: function process(traffic) {
                var params;
                var obj;

                traffic.request.queryString.some(({name, value}) => {
                    if (name === 'data') {
                        params = decodeURIComponent(value);
                        return true;
                    }
                });

                if (!params) {
                    return {};
                }

                try {
                    obj = JSON.parse(atob(params));
                } catch (e) {
                    obj = {};
                }

                obj.properties.event = obj.event;

                return obj.properties;
            }
        };
    } catch (e) {}
})();
```

2. Mixpanel Processor V2
```javascript
function getProcessor() {
    return {
        name: 'Mixpanel',
        namespace: 'mixpanel',
        process: function process(traffic) {
            var params;
            var obj;

            traffic.request.queryString.some(({name, value}) => {
                if (name === 'data') {
                    params = decodeURIComponent(value);
                    return true;
                }
            });

            if (!params) {
                return {};
            }

            try {
                obj = JSON.parse(atob(params));
            } catch (e) {
                obj = {};
            }

            obj.properties.event = obj.event;

            return obj.properties;
        }
    };
}
```

To put it in words, in V2:

1. The processor is represented as a `getProcessor` function.
2. The object that was assigned to a namespaced variable `window.diver.processors` in V1 is now returned in the `getProcessor` function.
3. There is no need to worry about catching errors thrown by the processor as the extension will handle them.
