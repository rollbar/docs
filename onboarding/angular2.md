## Installation

Install the Rollbar <a href="https://github.com/rollbar/rollbar.js" target="_blank" rel="noopener">rollbar.js</a> notifier using npm:

```bash
$ npm install --save rollbar
```

## Configuration

Import rollbar into your app and configure it to catch uncaught exceptions:

```
import * as Rollbar from 'rollbar';
import { BrowserModule } from '@angular/platform-browser';
import { NgModule, ErrorHandler } from '@angular/core';
import { AppComponent } from './app.component';

const rollbarConfig = {
  accessToken: 'POST_CLIENT_ITEM_ACCESS_TOKEN',
  captureUncaught: true,
  captureUnhandledRejections: true,
};

@Injectable()
export class RollbarErrorHandler implements ErrorHandler {
  constructor(private injector: Injector) { }
  handleError(err:any) : void {
    var rollbar = this.injector.get(Rollbar);
    rollbar.error(err.originalError || err);
  }
}

@NgModule({
  imports: [ BrowserModule ],
  declarations: [ AppComponent ],
  bootstrap: [ AppComponent ],
  providers: [
    { provide: ErrorHandler, useClass: RollbarErrorHandler },
    { provide: Rollbar,
      useFactory: () => {
        return new Rollbar(rollbarConfig)
      }
    }
  ]
})
export class AppModule { }

```

## Send a test error

Run the following command in your Javascript console.  Rollbar should catch the error and send it to your account:

```bash
window.onerror("TestError: Hello world", window.location.href)
```
