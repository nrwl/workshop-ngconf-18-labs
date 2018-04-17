# Lab: Service Workers

## Time: 36 hours

Enable service worker in your application.

Run console command to update angular CLI settings:

```console
ng set apps.0.serviceWorker=true
```

Create new file:

```ts
import { ServiceWorkerModule } from '@angular/service-worker';
ServiceWorkerModule.register('/ngsw-worker.js', {enabled: environment.production})
```

```json 
apps/customer-portal/ngsw.json:
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

## Next Lab
Go to Optimizing Performance Lab #4: [Universal](lab-4.md)
