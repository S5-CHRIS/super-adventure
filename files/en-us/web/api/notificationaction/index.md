---
title: NotificationAction
slug: Web/API/NotificationAction
browser-compat: api.NotificationAction
---
{{APIRef("Web Notifications")}}{{AvailableInWorkers}}{{securecontext_header}}

The `NotificationAction` dictionary defines the members that can be specified for the `actions` option of the second argument for the [`showNotification()`](/en-US/docs/Web/API/ServiceWorkerRegistration/showNotification) method and [`Notification()`](/en-US/docs/Web/API/Notification/Notification) constructor, representing actions the user can choose from to interact with notifications.

Browsers expose the specified actions to the user asynchronously, through the user interface that displays the actions may vary across platforms.

## Properties

### Instance properties

These properties are available only on instances of the `Notification` object.

- {{domxref("NotificationAction.action")}} {{readonlyinline}}
  - : The name of the action, which can be used to identify the clicked action.
- {{domxref("NotificationAction.title")}} {{readonlyinline}}
  - : The string describing the action that is displayed to the user.
- {{domxref("NotificationAction.icon")}} {{readonlyinline}}
  - : The URL of the image used to represent the notification when there is not enough space to display the notification itself.

## Example

Notifications can fire {{Event("notificationclick")}} events on the {{domxref("ServiceWorkerGlobalScope")}}.

Here a service worker shows a notification with a single "Archive" action, allowing users to perform this common task from the notification without having to open the website. The user can also click the main body of the notification to open their inbox instead.

```js
navigator.serviceWorker.register('sw.js');
Notification.requestPermission(function(result) {
  if (result === 'granted') {
    navigator.serviceWorker.ready.then(function(registration) {
      registration.showNotification("New mail from Alice',
        actions: [
          {
            action: 'archive',
            title: 'Archive'
          }
        ]
      )};
    )};
});

self.addEventListener('notificationclick', function(event) {
  event.notification.close();
  if (event.action === 'archive') {
    // Archive action was clicked
    archiveEmail();
  } else {
    // Main body of notification was clicked
    clients.openWindow('/inbox');
  }
}, false);
```

## See also

- [Using the Notifications API](/en-US/docs/Web/API/Notifications_API/Using_the_Notifications_API)
