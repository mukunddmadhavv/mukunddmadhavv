# Visitor counter

The header in `index.html` shows a shared visitor count to the left of the light toggle. It uses [CountAPI](https://countapi.mileshilliard.com/) for storage, so the site remains static and needs no backend deployment, account, or API key. The first visit creates the counter automatically; it starts counting from this addition, with no historical visit data.

- A random visitor token is saved in localStorage before the first increment. The token stays in the browser; it is not an API credential and is not sent to the service.
- Subsequent visits and refreshes read the shared total without incrementing it. Web Locks serialize simultaneous tabs in supported browsers.
- When localStorage is blocked, the counter is read-only. Network errors show `—` rather than an invented number.
- The token is retained after a failed or interrupted request: the service might already have counted it. This avoids duplicate increments on refresh, but a failed first request can leave a visitor uncounted.

This is an approximate unique-browser count, not exact people analytics. Clearing storage, using a different browser/device, or a new private-browsing session can count again. Public counters can be modified by anyone who knows their key, and availability depends on the hosted service. A completely offline/localStorage-only solution cannot share a total across visitors.

The counter key is `mukunddmadhavv-portfolio-visitors-845c9c11`. Keep it stable to preserve the total. For development, mock the API or change `counterKey` to a separate test key so local visits do not affect the live total.
