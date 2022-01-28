# CourseKit Quick-Start Guide
## Part 1: Set up and deploy course site

CourseKit is the easiest way for developers to create fully-custom online courses using their favorite frontend tech stack. Thanks to the CourseKit headless API platform, you won’t need a server, just a static site and you’ll get all the features you’ll need to provide a rich course experience for your prospective students.

This guide will take you through the steps of setting up a working CourseKit site in around ten minutes! After that, you can go back and customize it how you want and fill in the content for your lessons so you’re ready to launch.

The guide is in three sequential parts:

1. **Part 1: Set up and deploy course site (this document)**
    1. **Create a CourseKit account**
    2. **Clone one of the site templates on GitHub**
    3. **Link your site to your account**
    4. **Deploy to Netlify**
2. [Part 2: Enable paid students with Stripe enrollment](./quick-start-part-2.md)
3. [Part 3: Add lesson content including Vimeo videos](./quick-start-part-3.md)

> **Note: if you need any help or have any questions be sure to join the [CourseKit Discord](https://discord.gg/ugXJFkw6hv).**

## What you’ll build in part 1

By the end of the first part of the guide, you'll have cloned a CourseKit static site template and deployed it to Netlify. This static site will display courses and lessons that can be edited from the dashboard. You'll be able to manually add students who can log in and take your course.

Here's what your site home page will look like:

![quick-start-1-5.png](assets/quick-start-1-5.png)

## Requirements

To use this guide you’ll need the following:

- GitHub account
- [Netlify account](https://netlify.com)
- Node & NPM installed
- [Netlify CLI](https://docs.netlify.com/cli/get-started/) installed

## Create a CourseKit account

The first thing we'll do is create a CourseKit school. Go to [https://dashboard.coursekit.dev](https://dashboard.coursekit.dev) and register for an account.

![quick-start-1-1.png](assets/quick-start-1-1.png)

After your account is created you’ll be taken to the CourseKit dashboard. If you click on the “Courses” tab you’ll be able to see your basic school information and your courses. 

> Note: there are already two test courses added by default to a new user’s account - *Photography for Beginners* and *Advanced Photography*. These courses provide dummy data you can play with and help you understand how courses set up in CourseKit. After you complete this quickstart you can, of course, customize these with your own content, or delete them altogether.

![quick-start-1-2.png](assets/quick-start-1-2.png)

Click the Photography for Beginners course and you’ll see it has four lessons attached.

![quick-start-1-3.png](assets/quick-start-1-3.png)

You may have questions about what some of the other fields are for. We'll utilize all of these fields later in the guide!

## Install site template

Now that you have an account with some test courses and lessons created, you'll want to create a course website where you courses will be displayed.

Rather than doing that from scratch, let's install this [site template](https://github.com/course-kit/nuxt-demo). This will allow us to get the basic features of a course set up now and come back later and customize the UI and UX to your taste.

> Note: as CourseKit is still new, we currently only have the [Nuxt (Vue.js)](https://github.com/course-kit/nuxt-demo) template available (more will be providing using other JavaScript frameworks). Even if you don't want to use Nuxt or Vue to create your course, I recommend you continue following this guide to get a feel for CourseKit and then build your own site later.

To install the template, first, make a fork by clicking the "Fork" button in the top right. It's important to do this so that you have your own private repo that you can deploy from.

![quick-start-1-4.png](assets/quick-start-1-4.png)

Once you've forked the template, open a terminal and clone the template on your computer:

```bash
$ git clone https://github.com/<your-github-account>/nuxt-demo.git
```

Now, change into the directory and install NPM modules.

```bash
$ cd nuxt-demo
$ npm i
```

## Add config

After the NPM modules are install, create a `.env` file where you can add environment variables for config.

```
$ touch .env
```

Firstly, set the `NODE_ENV` variable to `development` so that our site uses development features and the CourseKit API realizes we're in test mode. You'll also need to set the `COURSEKIT_SCHOOL_ID` here so CourseKit knows which school to link this site to. 

> You can find your school ID in the dashboard on the "Courses" page.

*.env*

```
NODE_ENV=development
COURSEKIT_SCHOOL_ID=<your school ID>
```

Now save the .env file.

## Run dev server

In this guide, we'll be using Netlify to deploy our course site. You'll need the [Netlify CLI](https://docs.netlify.com/cli/get-started/) installed as we'll be using several CLI features and commands. 

Let's now run a dev server:

```
$ netlify dev
```

After the dev server finishes compiling, Netlify CLI will open your site in the browser. If you've configured it correctly, the home page will display your two courses.

> Note: you will need to use the default port of 8888 for the dev server otherwise the redirect URLs in the dashboard will be wrong (redirect URLs will be explained later in the guide).

![quick-start-1-5.png](assets/quick-start-1-5.png)

Now, take a look around your site. Click you courses and see the main course page, as well as all the lessons.

![quick-start-1-6.png](assets/quick-start-1-6.png)

You'll notice that the lesson content cannot be viewed without logging in as a student. If you click the **login** button in the navigation bar (top right), you’ll be taken to the login screen:

![quick-start-1-7.png](assets/quick-start-1-7.png)

We haven't yet added any student accounts, though, so let's do that now.

## Enrolling test students

To enroll a student in one of your courses, you will likely get them to pay for your course via an ecommerce platform like Stripe or Gumroad. After they've paid, you can use a webhook to add them to CourseKit with the API. 

We'll be setting up Stripe payments in part 2 of this guide. For now, you can add students to your courses manually via the dashboard.

Go to **Students tab** of the dashboard and click the add (plus) button where you can enter a name, email, and select a course. You'll should also tick the checkbox indicating that the student should be redirected to the development site after login rather than the production site.

> Note 1: you'll need to use an email address that you can access since students require email activation. However, the email should be different to your CourseKit user email. If you don't have extra email addresses, an easy way is to append `+<some string>` to your email prefix e.g. *yourname+somestring@domain.com*. This email should automatically be aliased to your current inbox.

![quick-start-1-19.png](assets/quick-start-1-19.png)

After you've added a student, you'll see them in your student list with status "PENDING". This means they've been sent an activation email and will now need to create an account.

![quick-start-1-9.png](assets/quick-start-1-9.png)

You should now receive the activation email. This email contains a unique URL that allows the student to create an account and enroll in the course.

![quick-start-1-10.png](assets/quick-start-1-10.png)

Click the link, and you'll be asked to register for the course. To re-iterate, this is not the same login as the dashboard - this is the login for student accounts so create a unique account here.

![quick-start-1-11.png](assets/quick-start-1-11.png)

Once you've created a student account you'll be redirected to the course home page.

> Note: if the redirect failed, you either didn't use port 8888 for your site or you didn't check the "Redirect to dev homepage URL" option when you enrolled the student!

![quick-start-1-12.png](assets/quick-start-1-12.png)

Returning to the student tab of the dashboard, refresh the page and you should now see the student status has gone from "PENDING" to "ACTIVE". This means they now have an active enrollment in the specified course.

![quick-start-1-13.png](assets/quick-start-1-13.png)

## Logged in features

Now that you're logged in as a student, click around your site and you'll see a variety of features you couldn't see previously. Most notably, if you click a lesson page you should now be able to see the lesson content!

All the lessons of the dummy courses have a test Vimeo video and some lorem ipsum text. In part 3 of the guide, we'll see how to customize these.

![quick-start-1-14.png](assets/quick-start-1-14.png)

Go ahead and experiement with the site - play the video, complete the lessons, etc. And keep in mind all the content and site behavior can be customized by modifying the code of your template. If you're interested in how to do this, check out the [CourseKit JavaScript client](https://github.com/course-kit/client).

## Deploy to Netlify

In the last section of this guide we'll deploy the site to Netlify so it is publicly available for your students to use. 

We'll first link your forked template to a Netlify site. To do this, go back to the terminal and kill your Netlify dev server (Ctrl + C) then run:

```
$ netlify init
```

Enter the following at subsequent prompts:

```
? What would you like to do? Create & configure a new site
? Team: <select your team>
? Site name (optional): <either choose something or leave blank>
? Your build command (hugo build/yarn run build/etc): npm run generate
? Directory to deploy (blank for current dir): dist
? Netlify functions folder: functions
```

Netlify should now print out your site details including the site URL.

Next, we'll need to set environment variables in the Netlify site.
```
$ netlify env:set COURSEKIT_SCHOOL_ID <your schoolId> 
$ netlify env:set NODE_ENV production
```

You’ll now need to rebuild the site for these environment variables to be incorported in the site build. To do this, you'll have to go the Netlify site and manually trigger a deploy:

![quick-start-1-15.png](assets/quick-start-1-15.png)

## Configure production site in dashboard

The final thing we need to do is tell the CourseKit dashboard about the production site - specifically, we have to set the redirect URLs.

Firstly, we'll set the school URL. To do this, go to the Courses tab, and click the edit button in the top right of the School pane.

Set the School URL (production) value to the URL of your Netlify site.

![quick-start-1-18.png](assets/quick-start-1-18.png)

Next, set the URL of each course. To do this, go to a course, and copy the course ID from the Course info pane. Then click the edit course button (top right of Course info pane).

Set the homepage URL (production) of your course to:

```
<your netlify url>/courses/<course id>
```

![quick-start-1-16.png](assets/quick-start-1-16.png)

Repeat this for the other course:

![quick-start-1-17.png](assets/quick-start-1-17.png)

> Note 1: these values are required so CourseKit knows where to redirect your student after they login to your school or enroll in a course. 

> Note 2: You can have both a development value and a production value for each redirect URL. We didn't have to set the development URL value because that was auto-generated as part of the dummy course data.

## Wrap up

With that done, you now have a deployed course site! In [part 2 of the quick start guide](./quick-start-part-2.md), we'll set up Stripe products so that students can enroll themselves by purchasing the course.
