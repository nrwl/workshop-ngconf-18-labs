# Lab: Angular Service Worker

## Time: 15 minutes

## Scenario
We want to cache all of our static assets to be served offline, and to load from cache even when we have network access. To do this, we'll leverage the official Angular Service Worker to automatically cache our static assets when building our app.

## Instructions

1. First, we want to indicate that our customer portal app should leverage Angular Service Worker by editing the app configuration in Angular CLI. We'll use Angular CLI to set the `serviceWorker` property of our customer portal app to "true" using the `ng set` command. Run `ng set apps.0.serviceWorker=true` in your terminal, then open `.angular-cli.json` to see the result. Find the customer-portal app in the `apps` array and look for the `serviceWorker` property, which should now be set to `true`.
1. Next, we'll want to add the ServiceWorkerModule to our App module so that it can manage the installation of the service worker. Open the app module for the customer portal, and import the `ServiceWorkerModule`: `import { ServiceWorkerModule } from '@angular/service-worker';`.
1. We'll add the `ServiceWorkerModule` to our App Module `imports`, and will give it two arguments. The first argument is the name of the service worker script which Angular CLI will generate (ngsw-worker.js by default). The second argument is a configuration object. We'll use the configuration object to specify that we only want the service worker to be active in production mode. This is because the service worker can affect the behavior of your application by not updating assets when you refresh. This can make for a confusing or frustrating development experience. Let's update our app module's imports to include the Service Worker: `imports: [..., ServiceWorkerModule.register('/ngsw-worker.js', {enabled: environment.production})]`
1. The final step to make our app ready for service workers is to provide a configuration object so the Angular Service Worker can know the right strategy for fetching and caching assets. Below is the default configuration if generating a new project with the `--service-worker` flag with Angular CLI:
```json
{
  "index": "/index.html",
  "assetGroups": [{
    "name": "customer-portal",
    "installMode": "prefetch",
    "resources": {
      "files": [
        "/favicon.ico",
        "/index.html"
      ],
      "versionedFiles": [
        "/*.bundle.css",
        "/*.bundle.js",
        "/*.chunk.js"
      ]
    }
  }, {
    "name": "assets",
    "installMode": "lazy",
    "updateMode": "prefetch",
    "resources": {
      "files": [
        "/assets/**"
      ]
    }
  }]
}
```
1. Create a new file at `apps/customer-portal/ngsw.json` and paste the default config.
1. Now we'll create a new npm script to build our application with service worker support. Angular CLI will not actually serve an application with the service worker enabled, because of the aforementioned impaired development experience. So to test our service worker, we'll need to build the app and serve it with another server. For Angular CLI to generate our service worker, we just need to build with the `--prod` flag. And we'll use `live-server` to serve the app locally, with a proxy to our server. Add the following script to package.json: `customer-portal:service-worker": "ng build --prod -a=customer-portal && live-server dist/apps/customer-portal --proxy=/api:http://localhost:3000/api`
1. Now let's start our backend server, then build and test our app: `npm run server`. And in a new terminal window, run: `npm run customer-portal:service-worker`. Your browser should automatically be opened to the app.
1. If you're not already in the Chrome browser, open it now. Then open Chrome Devtools and select the "Application" tab. Select "Service Workers" on the side nav of the Application tab if it's not already selected. You should see the service worker for the application installed. From this pane, you can manage the service worker, or unregister it.
1. To see the Service Worker do its job, go to the "Network" pane in Chrome Developer Tools and check the "offline" checkbox. Now refresh the page, and you should see the page more or less load without issues. Look at all of the requests in the Network tab, and they should all indicate that they were loaded from the service worker.
1. With service worker added, we can run a Lighthouse audit again and see the results. Though you may notice that running Lighthouse from within Chrome Developer Tools doesn't honor the service worker cache, and will not show very impressive timings. If you install the Lighthouse Chrome Extension, and run the audit from the extension, it seems to honor the Service Worker more consistently. With the Chrome extension, the time to first paint and time to interactive should both be significantly better. Search for "Lighthouse Chrome Extension" to find and install it.