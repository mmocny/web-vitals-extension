# Experimental Fork of Web Vitals Chrome Extension (alpha)
*A Chrome extension to measure [experimental Layout Shift variants](https://github.com/mmocny/web-vitals/tree/lsn) of Web Vitals metrics* 

This project is a temporary fork of [GoogleChrome/web-vitals-extension](https://github.com/GoogleChrome/web-vitals-extension).  You should look there first unless specifically testing the experimental Normalized Layout Shift metric values.

<img src="media/cwv-extension-screenshot.png">

<h3 id="install">Installation Instructions</h3>

<h4 id="install-master">Install from master</h4>

**Google Chrome**
1. Download this repo as a [ZIP file from GitHub](https://github.com/mmocny/web-vitals-extension/archive/experimental-ls.zip).
1. Unzip the file and you should have a folder named `web-vitals-extension-experimental-ls`.
1. In Chrome go to the extensions page (`chrome://extensions`).
1. Enable Developer Mode.
1. Drag the `web-vitals-extension-experimental-ls` folder anywhere on the page to import it (do not delete the folder afterwards).

## Usage

### Detailed drill-down

<img src="media/cwv-extension-drilldown.png" width="75%">

Clicking the Ambient badge icon will allow you to drill in to the individual metric values. In this mode, the extension will also say if a metric value `might change` or requires a user action.

For example, First Input Delay requires a real interaction (e.g click/tap) with the page and will be in a `waiting for input` state until this is the case. We recommend consulting the web.dev documentation for [LCP](https://web.dev/lcp), [CLS](https://web.dev/cls) and [FID](https://web.dev/fid) to get an understanding of when metric values settle.

In a future release, the drill-down will also include aggregate field performance data from PageSpeed Insights and the Chrome User Experience Report.

### Overlay

<img src="media/cwv-extension-overlay.png" width="75%">

The overlay displays a Heads up display (HUD) which overlays your page. It is useful if you need a persistent view of your Core Web Vitals metrics during development. To enable the overlay: 

* Right-click on the Ambient badge and go to Options.
* Check `Display HUD overlay` and click 'Save'
* Reload the tab for the URL you wish to test. The overlay should now be present.

## Contributing

Contributions to this project are welcome in the form of pull requests or issues. See [CONTRIBUTING.md](/CONTRIBUTING.md) for further details.

If your feedback is related to how we measure metrics, please file an issue against [web-vitals](https://github.com/GoogleChrome/web-vitals) directly. 

### How is the extension code structured?

* `src/browser_action/vitals.js`: Script that leverages WebVitals.js to collect metrics and broadcast metric changes for badging and the HUD. Provides an overall score of the metrics that can be used for badging.
* `src/bg/background.js`: Performs badge icon updates using data provided by vitals.js. Passes along
data to `popup.js` in order to display the more detailed local metrics summary.
* `src/browser_action/popup.js`: Content Script that handles rendering detailed metrics reports in the pop-up window displayed when clicking the badge icon.
* `src/options/options.js`: Options UI (saved configuration) for advanced features like the HUD Overlay

## FAQ

**Who is the primary audience for this extension?**

The primary audience for this extension is developers who would like instant feedback on how their pages are doing on the Core Web Vitals metrics during development on a desktop machine.

**How should I interpret the metrics numbers reported by this tool?**

This extension reports metrics for your desktop or laptop machine. In many cases this hardware will be significantly faster than that of the median mobile phone your users may have. For this reason, it is strongly recommended that you test using tools like [Lighthouse](https://developers.google.com/web/tools/lighthouse/) and on real mobile hardware (e.g via [WebPageTest](https://webpagetest.org/easy)) to ensure all your users there have a positive experience.

**What actions can I take to improve my Core Web Vitals?**

We are making available a set of guides for optimizing each of the Core Web Vitals metrics if you find your page is not passing a particular threshold:

* [Optimize CLS](https://web.dev/optimize-cls)
* [Optimize LCP](https://web.dev/optimize-lcp)
* [Optimize FID](https://web.dev/optimize-fid)

Lighthouse 6.0 final will also include additional actionability audits for these metrics. They will answer questions like:

* What element was identified as the Largest Contentful Paint?
* What elements experienced a shift and contributed to Cumulative Layout Shift?

We envision users will use the extension for instant feedback on metrics (for their desktop machine) but will then go and do a Lighthouse audit for (1) a diagnostic view of how these metrics look on a median mobile device and (2) specifically what you can do to improve.

## License

[Apache 2.0](/LICENSE)