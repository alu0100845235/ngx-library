# NgxCookiebot

An Angular wrapper around the [Cookiebot](https://www.cookiebot.com/) SDK.

## Installation
```
npm i ngx-cookiebot-angular7 -S
```

## Setup

### Prerequisites
A Cookiebot account.

### 1. Export / import script

```typescript
// shared.module.ts
import { NgxCookiebotModule } from 'ngx-cookiebot-angular7';

@NgModule({
  exports: [
    NgxCookiebotModule
  ]
})
```

```typescript
// app.module.ts
import { NgxCookiebotModule } from 'ngx-cookiebot-angular7';
import { CookiebotConfig } from '@config/cookiebot.config';

@NgModule({
  imports: [
    NgxCookiebotModule.forRoot(CookiebotConfig)
  ]
})
```

### 2. Configure service
Configure the service according to the [Cookiebot developer docs](https://www.cookiebot.com/en/developer/).

```typescript
// cookiebot.config.ts
import { NgxCookiebotConfig } from 'ngx-cookiebot-angular7';

export class CookiebotConfig extends NgxCookiebotConfig {
  blockingMode: 'auto' | 'manual' | string;
  cbId: string;
  culture?: string;
  framework?: string;
  level?: string;
  type?: string;
}
```

## Usage

### Consent box
The script will now automatically append itself to the `head` tag, which in turn will prompt the cookie consent box.

To interact with the "cookiebot" object, NgxCookiebot comes with a service that exposes it, which is ready for use after the service is ready (the script is injected):

```typescript
// whatever.ts
...
constructor(private _cookieBotService: NgxCookiebotService) {}
...
this._cookieBotService.onServiceReady$.pipe(
  filter((ready: boolean) => {
    return ready;
  })
).subscribe(() => {
  // this._cookieBotService.cookiebot is available
});
...
```

Reference the [Cookiebot docs](https://www.cookiebot.com/en/developer/) for a list of properties, methods and callbacks available through the cookiebot object. 

If you prefer to use observables, the NgxCookiebotService exposes an observable for every available method and callback on the cookiebot object:

#### Methods

| Method                            | Observable            |
|-----------------------------------|:-------------------------:|
| CookiebotOnConsentReady           | onConsentReady$           |
| CookiebotOnLoad                   | onLoad$                   |
| CookiebotOnAccept                 | onAccept$                 |
| CookiebotOnAccept                 | onAccept$                 |
| CookiebotOnDecline                | onDecline$                |
| CookiebotOnDialogInit             | onDialogInit$             |
| CookiebotOnDialogDisplay          | onDialogDisplay$          |  
| CookiebotOnTagsExecuted           | onTagsExecuted$           |

#### Callbacks

| Callback                          | Observable                |
|-----------------------------------|:-------------------------:|
| CookiebotCallback_OnLoad          | onLoadCallback$           |
| CookiebotCallback_OnAccept        | onAcceptCallback$         |
| CookiebotCallback_OnDecline       | onDeclineCallback$        |
| CookiebotCallback_OnDialogInit    | onDialogInitCallback$     |
| CookiebotCallback_OnDialogDisplay | onDialogDisplayCallback$  |
| CookiebotCallback_OnTagsExecuted  | onTagsExecutedCallback$   |

Usage example:
```typescript
// whatever.ts
...
this._cookieBotService.onConsentReady$.subscribe(
  // Consent ready
  console.log(this._cookieBotService.cookiebot.consent)
)
...
```

### Cookie declaration
The NgxCookiebot package exposes a component to insert the cookie consent declaration. 
Use the component where you want the declaration to appear: 

```
// my.component.html

<ngx-cookiebot-declaration></ngx-cookiebot-declaration>
```

## License
MIT © [Hallo Verden](https://github.com/halloverden)

## Change log

### 1.0.7
- Transpile to es5
- Added change log

### 1.0.6
- Changes in documentation

### 1.0.5
- Changes in documentation

### 1.0.4
- Changes in documentation

### 1.0.3
- Initial version
