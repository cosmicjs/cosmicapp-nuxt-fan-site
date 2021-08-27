# cosmic-nuxt-fan-site
This is a Nuxt App built using Cosmic as it's Headless CMS.  It utilizes Apollo to access the Cosmic v3 Graph QL.  It uses Tailwind CSS as the css framework.  It utilizes Cosmic's built integration with imgix to build out responsive images as well as advances use cases such as gif to mp4, og image optimization, and blending with text.

## Adding Content to Cosmic

You are going to first want to add some content to Cosmic for your fan site or whatever site you are making.  You will see several buckets in Cosmic to add content to.  Let's start with the homes bucket, for your home page.

<img src="https://tom.imgix.net/cosmic_buckets.png?h=450&auto=format">

Each item you add in the homes bucket will reflect a different section you can click into on your home page.  It's important to think about the organization of your site now, because this is what will enable that.  In the example, I make a Loki site and created three sections: 
*Episodes (a section to look at each episode from the show)
*Lokis (a section to look at each Loki variant from the show)
*About (an about page)

These sections have very limited info needed. Just a title and an image. Their names are important, because this will become the routes for each section in your nuxt app that you will be updating. 

<img src="https://tom.imgix.net/cosmic_home_bucket.png?h=450&auto=format">

You will now want to create Cosmic buckets for each section you made.  In the template, you already have the three I created, episodes, heroes, and homes.  But you may want to edit or add additional ones. These buckets will allow you to add content to each of those sections you started creating.

When you create a cosmic bucket, select them as a multiple bucket at the top. This is because you are going to enter multiple entries.

<img src="https://tom.imgix.net/cosmic_bucket_settings1.png?w=450&auto=format">

Then leave the default settings of title, slug, content alone.  You will then most likely want to add an image to the metadata area and anything else you may want to display.  In my examples, I added a heroimage and an episode_number.  

<img src="https://tom.imgix.net/cosmic_bucket_settings2.png?w=450&auto=format">

You can go ahead and finish making these buckets and add some content to them.  

## Apollo GraphQL Queries with Cosmic

Once you have some content in your Cosmic buckets, you now need to make a few updates to the Nuxt app in order to display your content.  You will need to update the GraphQL Queries we are doing to Cosmic.  For these queries, I am using Apollo.  You will find 5 Queries in a apollo/queries folder.

<img src="https://tom.imgix.net/cosmic_apollo_folder.png?h=450&auto=format">

Here is an example of what one of the queries looks like: 

```
{
  getObjects(
    bucket_slug: "",
    read_key: "",
    input: {
        query: { type: "episodes" }
    }
  ) {
		objects {
      id
	  content
	  title
      metadata
      slug
		}
    }
}
```

You will need to update the bucket_slug and the read_key.  Also, if you are adding additional or Modifying Cosmic Buckets, you would add the name of the bucket to the query type.  You can find the bucket_slug and read_key in your Cosmic settings, API Access.  We are not using the write_key, so the rest of these items are not a concern to publicly be seen. That's why they are not obscured in my screenshot or added to .env files or anything.

<img src="https://tom.imgix.net/cosmic_api_access.png?w=450&auto=format">

If you do want to do a bit of a deeper dive on the GraphQL, Cosmic does have a simple GraphQL playground.  Just click on one of your Cosmic Buckets, then next to the name of it, you will see Developer Tools. This can help you debug items and see what the values you are going to get from each query.  The reason I am choosing to use the GraphQL is to ensure that I don't get large payloads by accessing all of the content of my Cosmic site on each page load. The GraphQL allows me to get pretty specific and only ask for certain content.  In my example query above, I'm only asking for the id, content, title, slug, and metadata of the items in the episodes section.  The metadata is the additional items we added, like the hero image or the episode number.

<img src="https://tom.imgix.net/cosmic_developer_tools.png?w=450&auto=format">

Once you have filled in the bucket_slug and the read_key, your queries should look like this: 

```
{
  getObjects(
    bucket_slug: "loki-webinar-production",
    read_key: "TMNjyVSNbfE75hA7q92OTZex74Ye5NuIn20DRWNroYgRGj4y9Y",
    input: {
    query: {
      type: "episodes"
    }
  }) {
		objects {
      id
	  content
	  title
      metadata
      slug
		}
    }
}
```

You can also certainly use my bucket_slug and read_key if you would like to just see the content I did in my demo app.

## Deploy Via Vercel

At this point, you actually don't need to make any additional changes.  You can run the app locally using `yarn dev` or deploy it easily via Vercel or whatever tool you prefer.  There are certainly additional tweeks we can make to the site which I will go over below if you would like as well.  I have added a vercel.json file to this template, so it is extremely simple to deploy the site. I find it easiest to push the site to Github and connect your Github with Vercel.  You can then just click `New Project` in Vercel and choose the git repo you pushed the project to. No other adjustments or settings need to be added. The settings of the vercel.json ensures everything will work smoothly.

## Customizations to Routes



## Build Setup

```bash
# install dependencies
$ yarn install

# serve with hot reload at localhost:3000
$ yarn dev

# build for production and launch server
$ yarn build
$ yarn start

# generate static project
$ yarn generate
```


