## notify.js

This is a simple, lightweight notification UI package for web applications.

_Note:_ This library requires [@itsmistad/network.js](https://github.com/itsmistad/network.js) for server-to-client notifications. Without `network.js`, `notify.initNetwork` will not work.

### Importing

#### CDN

In your .html file, add this to your `<head>` tag
```html
<!-- Required Dependencies --->
<script src="https://code.jquery.com/jquery-3.4.1.min.js"></script>
<!-- Optional Dependencies --->
<script src="https://cdnjs.cloudflare.com/ajax/libs/aspnet-signalr/1.1.4/signalr.min.js"></script>
<script src="https://raw.githubusercontent.com/itsmistad/network.js/master/network.js"></script>
<!-- notify.js --->
<script src="https://raw.githubusercontent.com/itsmistad/notify.js/master/notify.js"></script>
```

### Default Options

`targetSelector: 'body'`
> What element selector to use when adding the notification using the "targetMethod"

`targetMethod: 'append'`
> How to add the notification to the "targetSelector" ('prepend', 'append', 'before', and 'after')

`class: 'notify-popup'`
> The string list of style classes for the element's class attribute

`header: ''`
> The html header of the notification ('' = disabled and hidden)

`subheader: ''` 
> The html subheader of the notification ('' = disabled and hidden)

`body: ''`
> The html body of the notification ('' = disabled and hidden)

`closeButton: true` 
> Toggles the close button

`timeout: 0` 
> How long (in ms) until the notification closes (0 = disabled)

`fadeOutDuration: 400`
> How long (in ms) does the fade out animation last

`fadeInDuration: 800`
> How long (in ms) does the fade in animation last

`layer: defaultNotificationLayer`
> The z-index layer of the notification

`onStartClose: () => { }`
> The event that gets called when the notification starts closing 

`onClose: () => { }`
> The event that gets called when the notification is fully closed

`handleAsStack: false` 
> Toggles handling FIFO notification stacks by sliding down the notifications after an older sibling is closed

`maxInStack: 4`
> The maximum amount of notifications that can be added to the stack at once when "handleAsStack" is true

`sound: ''`
> The sound name that was specified with "notify.initSound(name, file)"

`buttons: []`
> The list of button objects to insert into the notification form

```js
buttons: [
    {
        text: 'OK',
        class: '', // The string list of style classes for the element's class attribute
        action: button => { }, // The event that gets called when the button is clicked
        close: true // Toggles whether the button closes the notification when clicked
    }
]
```

### Usage

Initialize a notification sound:
`notify.initSound([file path])`
```js
notify.initSound('/path/to/mp3/');
```

Connect to the server's `/notify` hub:
`notify.initNetwork()`
```js
notify.initNetwork();
```

Toggle the notification overlay layer:
`notify.overlay([toggle state], [optional fade duration], [optional opacity])`
```js
network.overlay(true, 300, 0.3);
```

Create a notification:
`notify.me([options object])`
```js
var notification = notify.me({
    header: 'Notification Header',
    subheader: 'Nice.',
    body: 'This is a test!',
    onStartClose: () => {
        notify.overlay(false);
    },
    closeButton: true
});
notify.overlay(true);

/*
 * notification contains the following properties:
 * - id (element id)
 * - $ (jQuery object)
 * - options (the options it was originally invoked with)
 * - close() (closes the notification)
 */
```