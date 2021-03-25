# Proxy Pattern 

This sample shows you how to deploy all your dependencies in Okteto Cloud, while developing the rest of your application locally. 

1. Run `okteto up`. This will deploy the proxy instance. This instance will act as a proxy for all your stores, redirecting traffic from varnish to your local machine, and from your local machine to the mongo and redis. You can run this command from an empty folder, since we are not going to synchronize code.

        okteto up 

1. Start a local process that listens on port `8080`. 

        python -m http.server 8080

1. Deploy your dependencies in Okteto Cloud. This will deploy varnish, redis, and mongo.

        okteto stack deploy --build

1. Send a request to the varnish service (replace rberrelleza with your GithubID). The request will hit varnish, then it will go to `proxy:8080`, and from there, to your local machine.

        curl https://proxy-rberrelleza.cloud.okteto.net/

1. Mongo and Redis will be accessible over localhost, so you can use tools like `redis-cli`and `mongocli` to access the stores.