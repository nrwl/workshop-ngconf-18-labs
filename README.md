# Lab Instructions for Nx Workshop

## Organizing Code in a Workspace
1. [Create an App and a Lib](organizing-code-in-a-workspace/lab-1.md)
1. [Create a Lazy Loaded UI Lib](organizing-code-in-a-workspace/lab-2.md)
1. [Public APIs for Libs](organizing-code-in-a-workspace/lab-3.md)
1. [Run the Build Command and NPM Scripts](organizing-code-in-a-workspace/lab-4.md)

## Performance

1. [Lighthouse Analysis](optimizing-performance/lab-1.md)
1. [Source Map Explorer](optimizing-performance/lab-2.md)
1. [Service Workers](optimizing-performance/lab-3.md)
1. [Angular Universal](organizing-code-in-a-workspace/lab-4.md)

----

<br/>

### Running the Application

Run the following command(s) in individual terminals:

```console
npm run server
npm run customer-portal
```


*  Open the **Customer Portal** application with the browser: http://localhost:4203
*  Confirm the **Node Server** is running with browser page:  http://localhost:3000/api/tickets

If you already have one(s) running and you need to restart, you can stop the run with `ctrl+c`.

#### Restarting the App Server

Sometimes a change to TypeScript interfaces or adding new `*.ts` files <u>will not get picked up</u> by the watch processes. In such cases, you may need to stop/restart these... if you feel your code is correct but you are getting an error.


<br/>

----
