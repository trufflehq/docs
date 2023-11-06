# Embed Config

Apps can have multiple Embeds, whose configuration is specified as an array in the `embeds` property inside the `truffle.config.mjs` file.

This embed config is the same config that you can see inside the Truffle dev tools in browser.

## Properties

`slug` - a slug string to identify the embed.

`url` - the url that gets iframed when the embed is displayed

`contentPageType`&#x20;



| value of ContentPageType | Where does the embed display                                                |
| ------------------------ | --------------------------------------------------------------------------- |
| youtubeLiveNow           | youtube streams that are currently live                                     |
| youtubeLiveUpcoming      | scheduled youtube livestreams                                               |
| youtubeLiveVod           | vods for youtube livestreams                                                |
| youtubeVideo             | youtube videos                                                              |
| youtube                  | any youtube video, livestream, scheduled livestream, or vod                 |
| twitch                   | a streamer's twitch page                                                    |
| quickActions             | inside a creators quick action menu                                         |
| appManagement            | creator dashboard -> apps; it will appear when a creator clicks on your app |

#### Windowed Embeds

Define the `windowProps` property to have your embed show up in the sidebar!

`windowProps`  an object containing the following props

* `title` - listed in the window bar
* `tooltipDescription` - the text displayed when users hover over your embed icon
*   `initialDimensions` - an object representing the default dimensions of your windowed embed

    ```typescript
    {
      width: number;
      height: number;
    }
    ```
* `isResizable` - boolean; true means that users can resize your embed however they please
*   `resizeBounds` - optional, an object representing the smallest and largest dimensions that a user can scale the embed window

    ```typescript
    {
      minWidth: number; 
      maxWidth: number; 
      minHeight: number;
      maxHeight: number;
    }
    ```

#### Styles

`iconUrl` - an icon for your embed, we recommend using SVGs

`parentQuerySelector` - optional; the query selector for the element that will be the parent of the iframe. Defaults to `#above-the-fold` (below the video) on youtube (other defaults be used for different platform page types).

`defaultStyles` - optional; default css styles that will be applied to the iframe when it is first rendered on the page.

#### Misc

`isLoginRequired` - boolean; set to true if you need users to log in to use your embed

`deviceType` - optional; can be one of `desktop` or `mobile`; defaults to `desktop`.

`minTruffleVersion` - optional; minimum version of truffle (extension or mobile app) required to render the embed.

`maxTruffleVersion` - maximum version of truffle (extension or mobile app) allowed to render the embed.

`status` - optional; `published`, `experimental`, `disabled;` defaults to \`published\`. experimental embeds only render if the user has experimental mode enabled in the extension.

## Example

```typescript
export default {
  name: "@org/package",
  version: "1.0.0",
  apiUrl: "https://mycelium.truffle.vip/graphql",
  description: "Cool description, bro",
  embeds: [
    {
      slug: "cool-embed",
      url: "https://cool-embed.netlify.app",
      contentPageType: "youtubeLiveNow",
      parentQuerySelector: "#above-the-fold",
      defaultStyles: {
        width: "100%",
        height: "300px"
      }
    }
  ]
};
```

