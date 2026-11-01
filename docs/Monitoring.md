/metrics endpoints will be added to all services sequentially. This file serves as a note for the how-to's of defining the metrics endpoint.

As a starting point the '/metrics' endpoint was created for the **order service**:
* Middleware is used; this acts as a entrypoint to all subsequent api pathways defined in the service. All incoming user requests (to the service) is accepted by the middleware and then forwarded to the respective endpoint (via call_next); then records the result of the request and the elapsed time.

* The middleware is defined as an async function, it forwards the request to the real pathway and awaits for the response and records the time it took for the response.

* Any requests incoming onto the '/metrics' endpoint doesn't cause the request tracking logic to be run.

## Points to remember

* Lables split a single metric to many series which allows us to query the Prometheus server with fine-grained questions like "How many requests were responded with 500 error?". But unbound values (ex- user id at the end of a request path) should never be passed as this created a new time series for each combination in the route path.

* Labels are defined for example as HTTP_REQUESTS = Counter("http_requests_total","Total HTTP requests",["method", "route", "status"],) which allows the sorting of metrics through method, route and status.

* There's 3 main types of metrics tracked by Prometheus:
    ** Counter: (ex- number of all handled requests) these are numbers that only go up
    ** Gauge: (ex- number of active requests) these are numbers that can go either up or down
    ** Histogram: (ex- duration of a request)

**Only auth and inventory services will be monitored with Prometheus**