# NEFAC WordPress Training
This is a training project that will help you familiarize yourself with the [Faust.js](https://faustjs.org/) library and the WordPress API, through which we will use WordPress as a headless CMS for our NextJS website.
- **Required** by next meeting - https://faustjs.org/docs/tutorial/learn-faust/ (est. 1 hour)
  - In this tutorial, you'll download a template project with a local WordPress environment, set up the relevant plugins, and build a basic Faust.js app. The tutorial is very detailed, so by the end, you'll understand a lot of the essential concepts.
  - NOTE if you are on **Windows** please see the troubleshooting section!
- **Strongly recommended** additional tutorial - https://faustjs.org/docs/how-to/custom-blocks/ (est. 30 mins)
  - This tutorial shows how you can override the rendering of the Code Block which is provided by WordPress. However, the code is very similar for custom blocks we can create that are modeled after our own React components. This is something we will be doing often in the future.
  - You can skip part 6, but read through it so you can see a real use case for this
- If you are stuck, see the troubleshooting section below or ask for help!

## Resources
- [Faust.js](https://faustjs.org/) - The library/framework/plugin we'll be using to interface with WordPress
    - [Basic Setup Guide](https://faustjs.org/docs/how-to/basic-setup/)
    - [Project walkthrough](https://faustjs.org/docs/tutorial/learn-faust/)
    - [Discord server](https://faustjs.org/discord)
- [headless-wp](https://github.com/imarc/headless-wp/) - Example NextJS+Faust.js+WordPress project you can run locally
- [Perplexity thread](https://www.perplexity.ai/search/i-have-react-nextjs-experience-6bouvoroQ86JrAK920ek4Q) from my research on Faust.js that might answer some questions you have

## Troubleshooting
### Main Tutorial
- If you are on **Windows**, you will likely encounter an error when running `npm run wp-dev`. This is a bug and I have made issues on the relevant repositories to hopefully get it fixed. In the meantime, unfortunately, you may need to use [Windows Subsystem for Linux](https://learn.microsoft.com/en-us/windows/wsl/install) or [Docker Desktop](https://www.docker.com/products/docker-desktop/). Really sorry about the added complexity, it's supposed to work out of the box. Let me know if you need help setting up.
    - See https://github.com/WordPress/playground-tools/issues/375 and https://github.com/WordPress/wordpress-playground/issues/2217
- In the [Template Hierarchy](https://faustjs.org/docs/tutorial/learn-faust/#add-a-template) section of the tutorial, when you're told to copy and paste the `SingleTemplate.query` assignment into `wp-templates/page.js`, you also have to change all occurrences of "post" to "page" within the GraphQL query itself. This isn't explicitly written in the instructions, but the change is reflected in the included code.
- I was having an SSL issue when trying to [preview draft posts](https://faustjs.org/docs/tutorial/learn-faust/#2-preview-a-draft-post). I'm fairly certain it will work in production, so you can ignore that issue for now if you encounter it.

### Custom Blocks Tutorial
- In order to do this tutorial, within WordPress, you need to create a post (*not* a page) with a code block in it. Then, you'll need to modify the GraphQL query in `single.js` to also fetch information about code blocks in the post. This roughly aligns with the tutorial, but can be a little unclear.
- If you're reusing the same `single.js` from the first tutorial, you might include something like this in your template code to render the code block (import the `CodeBlock` component you wrote):
  ```js
  if (block.name === 'core/code') {
    return (
      <CoreCode attributes={block.attributes} />
    )
  }
  ```
