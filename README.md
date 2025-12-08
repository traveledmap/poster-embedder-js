<p align="center">
  <a href="https://www.traveledmap.com">
    <img src="https://www.traveledmap.com/images/logos/traveledmap-black.png" alt="Logo" width="160">
  </a>

<h3 align="center">TraveledMap's poster embedder SDK</h3>

  <p align="center">
    This repository contains the JavaScript library used to embed
    <a href="https://www.traveledmap.com">TraveledMap</a> poster's reselling widget
    directly inside any website (WordPress, Prestashop, Webflow, custom CMS, static websites…).
    <br />
    <br />
    <a href="https://www.traveledmap.com/posters/embed/configure/">View demos & configuration tool</a>
    ·
    <a href="https://github.com/TraveledMap/poster-embedder-js/issues">Report Bug</a>
  </p>
</p>


---

# Before getting started

- **Demos and configuration** are available on TraveledMap's dedicated page:
  👉 [here](https://www.traveledmap.com/posters/embed/configure)
- Don't hesitate to have a look at the [FAQ](#faq) or contact us by email if you need help.
- Creating posters requires either:
    - an active affiliation account that you can request [here](https://www.traveledmap.com/affiliates/request).
    - a direct partnership with TraveledMap. You can contact us at contact@traveledmap.com

---

# Table of Contents

* [Quick start](#quick-start)
* [Config](#config)
* [Examples](#examples)
* [FAQ](#faq)
* [Help](#help)

---

# Quick start

## 1. Add a container in your HTML

Choose where the widget should appear and create a container with a unique identifier and a defined height:

```html

<div id="traveledmap-poster" style="min-height: 650px; width: 100%;"></div>
```

---

## 2. Include the TraveledMap Poster SDK

```html

<script src="https://cdn.jsdelivr.net/gh/traveledmap/poster-embedder-js@latest/dist/traveledmap-poster.min.js"></script>
```

---

## 3. Instantiate the poster widget

Tip: To easily get the configuration object, use our [configuration page](https://www.traveledmap.com/posters/embed/configure)

```html

<script>
    const onLoad = function () {
        new TraveledMapPoster("#traveledmap-poster", {
            actions: ["CUSTOMIZE_AND_ORDER"],
            affId: "your-affiliate-id",
            userId: "your-user-id",
            templateId: "your-template-id",
            mapStyle: {default: "pastel-blue", isEditable: true},
            format: {default: "a3", availableFormats: ["a4", "a3", "a2"]}
        });
    };

    if (window.addEventListener) {
        window.addEventListener("load", onLoad, false);
    } else if (window.attachEvent) { // IE DOM
        window.attachEvent("onload", onLoad);
    } else {
        onLoad();
    }
</script>
```

---

## Config

All the following properties can be passed to `new TraveledMapPoster(selector, config)`.

| Property                         | Required | Default          | Description                                                                                                                                                                                         |
|----------------------------------|----------|------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **actions**                      | **Yes**  | `[]`             | Array of actions available to the user. Possible values (see below the table for more details): `CREATE_FROM_SCRATCH`, `CUSTOMIZE_AND_ORDER`, `SEND_ORDER_EMAIL`. Determines which buttons appear.  |
| **affId**                        | No       | `undefined`      | Affiliate identifier. Required if commissions or referral tracking are needed.                                                                                                                      |
| **userId**                       | No       | `undefined`      | Owner of the poster templates. Required when `templateId` is provided. If omitted and no template provided, the embed falls back to a poster **carousel mode**.                                     |
| **templateId**                   | No       | `undefined`      | Loads a predefined poster template. When set, the template's mapStyle overrides the default provided in configuration.                                                                              |
| **mapStyle.isEditable**          | No       | `true`           | Allows users to select a map style.                                                                                                                                                                 |
| **mapStyle.default**             | No       | `"pastel-blue"`  | Initial map style **only if no templateId is set**. Templates always override this value.                                                                                                           |
| **format.isEditable**            | No       | `true`           | Allows users to change the poster format.                                                                                                                                                           |
| **format.availableFormats**      | No       | `["a3","a2"]`    | List of selectable formats. Ignored if `format.isEditable = false`.                                                                                                                                 |
| **title.isEditable**             | No       | `true`           | Allows editing the poster title. Can really be edited when a template is used, however, you can pass this option to true when displaying the generic (no template) image, to for user incentive.    |
| **subtitle.isEditable**          | No       | `true`           | Allows editing the poster subtitle. Can really be edited when a template is used, however, you can pass this option to true when displaying the generic (no template) image, to for user incentive. |
| **background.isHidden**          | No       | `false`          | Hides the background texture behind the poster preview.                                                                                                                                             |
| **background.color**             | No       | `undefined`      | Custom background color applied behind the poster if `background.isHidden` is `true` (not affecting the poster itself). Any CSS color is valid.                                                     |
| **shouldHideFrame**              | No       | `false`          | Hides the decorative poster frame in the preview UI.                                                                                                                                                |
| **currency**                     | No       | Auto-detected    | Forces a specific currency. Not recommended: detection is usually correct.                                                                                                                          |
| **deliveryCountry**              | No       | Auto-detected    | Forces the shipping country. Not recommended: auto-detection is usually correct.                                                                                                                    |
| **reseller.id**                  | No       | `undefined`      | Used when multiple resellers are working with the same affiliateId and commissions must be routed to different accounts.                                                                            |
| **reseller.name**                | No       | `undefined`      | Used to include your brand when sending reminder emails: Defaults to affiliate name.                                                                                                                |
| **customerDetails.emailAddress** | No       | `undefined`      | Pre-fills the customer's email when using `SEND_ORDER_EMAIL`. If omitted, the UI asks for it.                                                                                                       |
| **customerDetails.sendOn**       | No       | Send immediately | Pre-fills the reminder date. Only applicable when `SEND_ORDER_EMAIL` is used.                                                                                                                       |

[//]: # (| **redirectToHost**               | No       | `undefined`     | If provided, the iframe requests a redirect of the embedding page &#40;host&#41; after the action completes &#40;e.g. after scheduling email&#41;.                                                                 |)
[//]: # (| **format.default**               | No       | `"a3"`          | Initial format **only if no templateId is set**. Templates override this.                                                                                                                          |)

[//]: # (| **title.default**                | No       | `undefined`     | Used **only when no templateId is set**.                                                                                                                                                           |)

[//]: # (| **subtitle.default**             | No       | `undefined`     | Used **only when no templateId is set**.                                                                                                                                                           |)

Here are the available actions :

| Action                | Description                                                                                                                                       |
|-----------------------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| `CREATE_FROM_SCRATCH` | Opens the poster builder without predefined template.                                                                                             |
| `CUSTOMIZE_AND_ORDER` | Opens builder with the given template.                                                                                                            |
| `SEND_ORDER_EMAIL`    | Sends or schedules a reminder email. To see the email, please use the [configuration helper](https://www.traveledmap.com/posters/embed/configure) |

---

# FAQ

### Where can I find my affiliateId (affId)?

You can find it inside your [TraveledMap affiliate dashboard](https://www.traveledmap.com/affiliates/dashboard).
Moreover, the [configuration helper](https://www.traveledmap.com/posters/embed/configure) has been created to prefill
the configuration with your data.

### Where can I find my userId?

You can find it inside the [configuration helper](https://www.traveledmap.com/posters/embed/configure) that has been
created to prefill
the configuration with your data.

### Where can I find the templateId?

You can find it inside the [configuration helper](https://www.traveledmap.com/posters/embed/configure) where you'll be
able
to select the template amongst your templates

### Which actions are available?

### How does the SDK work?

The SDK is a lightweight script that will create an iframe window, displaying a TraveledMap page that helps customize
and be redirected to the poster's purchase page.

---

# Help

Issues: https://github.com/TraveledMap/poster-embedder-js/issues  
Support: contact@traveledmap.com