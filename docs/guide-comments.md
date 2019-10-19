# Add comments to Gridsome

Adding comments to a static site can be easy, you have the option to use either external services that load an iframe into your site or applications that connect to your Github repository which commits the changes made on your site. We have listed some great services that integrate well with Gridsome.

## Disqus
Disqus is an external service that injects an iframe on your site, one easy way to use Disqus with Gridsome is to use the package [vue-disqus](https://github.com/ktquez/vue-disqus) that provides you with a custom component that you can use across your project.

#### Sign up on Disqus
First step is to sign up for an account on [Disqus](https://disqus.com/). When presented with the option you want to choose 'I want to install Disqus on my site'. Continue by filling in all necessary information about your site and when you are asked 'What platform is your site on?', pick 'Universal Code' at the bottom of the page. 

Complete the setup of your site and take note of your `Shortname` because this will be used later.

![shortname](https://i.imgur.com/Ui1aoYi.png) 

#### Install vue-disqus
You can use vue-disqus for easier implementation or use disqus directly, but this guide is using vue-disqus.

`yarn add vue-disqus`
or with npm
`npm install vue-disqus`

After it has been added to your package.json and installed you need to import vue-disqus in your `main.js` which is located directly in the `src` directory, and added to the vue instance. 

```js
import VueDisqus from 'vue-disqus'

export default function (Vue, { head })  {
  Vue.use(VueDisqus)
}
```

Now you are free to use the disqus component anywhere you want, simply use it like this:

```js
<vue-disqus shortname="mygridsomesite" :identifier="$page.post.title"></vue-disqus>
```

You need to provide a shortname which you can find on [Disqus](https://disqus.com/) under your site you configured after you signed up. You also need to provide an identifier, in this example we used the blogpost title from the GraphQL query.

Read more: [Disqus](https://disqus.com/)

## Vssue

[Vssue](https://vssue.js.org/guide/) is a Vue component / plugin, which can enable comments for your static pages. It stores comments in the issue system of code hosting platforms (e.g. Github, Gitlab, Bitbucket, Gitee, etc.)

#### Choose a platform and set up OAuth App

First, you should [choose a platform](https://vssue.js.org/guide/supported-platforms.html) to use and follow the guide to set up OAuth App. Here we take [GitHub](https://vssue.js.org/guide/github.html) for example.

#### Install vssue

Install Vssue and API package that you want to use:

```sh
npm install vssue @vssue/api-github-v3
```

#### Import in gridsome

Import Vssue in your `main.js`:

> See [Vssue docs](https://vssue.js.org/guide/getting-started.html) for how to set the options

```js
import Vssue from 'vssue';
import GithubV3 from '@vssue/api-github-v3';
import 'vssue/dist/vssue.css'

export default function (Vue) {
  Vue.use(Vssue, {
    api: GithubV3,
    owner: 'your-github-username',
    repo: 'your-github-repository',
    clientId: 'xxx',
    clientSecret: 'xxx',
  })
}
```

#### Use Vssue component in pages

Now you are free to use the `<Vssue />` component anywhere you want, simply use it like this:

```vue
<Vssue :title="$page.post.title" />
```

## Staticman
Staticman is an application that you connect to your Github repository which commits comments or any other type of user input to your site that you have configured.
Read more: [Staticman](https://staticman.net/)
