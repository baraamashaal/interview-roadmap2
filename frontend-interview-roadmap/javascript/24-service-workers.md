
# 24. Service Workers in JavaScript

## Quick Revision

A **service worker** is a script that your browser runs in the background, separate from a web page, opening the door to features that don't need a web page or user interaction. Key features include:

*   **Offline support:** Intercepting network requests and serving cached responses.
*   **Push notifications:** Receiving push messages from a server and displaying them to the user.
*   **Background sync:** Deferring actions until the user has a stable internet connection.

## Detailed Explanation

A service worker acts as a proxy between your web application and the network. It is a type of **web worker**, which means it runs on a separate thread from the main browser thread, so it won't block your UI.

### The Service Worker Lifecycle

A service worker has a lifecycle that is completely separate from your web page.

1.  **Registration:** You register the service worker in your main JavaScript file.
2.  **Installation:** The service worker is installed. This is a good time to cache static assets.
3.  **Activation:** The service worker is activated. This is a good time to clean up old caches.
4.  **Idle:** The service worker is now ready to handle events.

### Key Features and Use Cases

#### 1. Caching and Offline Support

Service workers can intercept network requests using the `fetch` event. This allows you to serve cached content when the user is offline.

**Caching Strategies:**

*   **Cache First:** Serve from the cache first, and if it's not there, go to the network.
*   **Network First:** Go to the network first, and if it fails, serve from the cache.
*   **Stale-While-Revalidate:** Serve from the cache and update the cache from the network in the background.

#### 2. Push Notifications

Service workers can listen for `push` events from a server and use the `showNotification()` method to display a notification to the user, even when the web page is not open.

#### 3. Background Sync

The Background Sync API allows you to defer actions until the user has a stable internet connection. For example, you could allow a user to send a message while offline, and the service worker will send it as soon as the connection is restored.

### Security

Service workers have a lot of power, so they are only available over **HTTPS**.

## Code Examples

### Registering a Service Worker

```javascript
// main.js
if ('serviceWorker' in navigator) {
  window.addEventListener('load', () => {
    navigator.serviceWorker.register('/service-worker.js')
      .then(registration => {
        console.log('ServiceWorker registration successful with scope: ', registration.scope);
      })
      .catch(error => {
        console.log('ServiceWorker registration failed: ', error);
      });
  });
}
```

### Caching Assets during Installation

```javascript
// service-worker.js
const CACHE_NAME = 'my-cache-v1';
const urlsToCache = [
  '/',
  '/styles/main.css',
  '/script/main.js'
];

self.addEventListener('install', event => {
  event.waitUntil(
    caches.open(CACHE_NAME)
      .then(cache => {
        console.log('Opened cache');
        return cache.addAll(urlsToCache);
      })
  );
});
```

### Serving from Cache

```javascript
// service-worker.js
self.addEventListener('fetch', event => {
  event.respondWith(
    caches.match(event.request)
      .then(response => {
        // Cache hit - return response
        if (response) {
          return response;
        }
        return fetch(event.request);
      })
  );
});
```

## Resources

*   **Article:** [MDN - Service Worker API](https://developer.mozilla.org/en-US/docs/Web/API/Service_Worker_API)
*   **Article:** [Introduction to Service Worker](https://developers.google.com/web/fundamentals/primers/service-workers)
*   **Video:** [The Service Worker Lifecycle - Google Chrome Developers](https://www.youtube.com/watch?v=gn9D3d-2w5E)
*   **Course:** [Offline Web Applications by Google](https://www.udacity.com/course/offline-web-applications--ud899)
