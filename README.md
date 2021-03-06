Heroku Buildpack: Info
======================

Display information about the build process.


Description
-----------

This buildpack doesn't do any transformations, it just displays various locations and their contents on the build dyno during the build of your app. It is useful to better understand the build process, for example, for creating a custom buildpack.

As a **summary**, when you do `git push heroku master`, then:

- your app directory is sent to a **build dyno** where it is placed in a certain directory
- the **slug compiler** running on the build dyno fetches the **buildpack**, set with `heroku buildpack:set <url>`, and executes its `detect`, `compile`, and `release` scripts
- your app directory, along with any transformations made by the `compile` script, (now called **"slug"**) is loaded as `/app` onto the production **dynos**, and the dynos are started


Usage
-----

Simply do

~~~bash
heroku buildpacks:set https://github.com/weibeld/heroku-buildpack-info.git
~~~

On the next `git push heroku master`, the Info buildpack will be used.

For more information on how to use custom buildpacks, see <https://devcenter.heroku.com/articles/third-party-buildpacks#using-a-custom-buildpack>.


Usage together with other buildpacks
------------------------------------

You can use multiple buildpacks at the same time as described on [https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app](
https://devcenter.heroku.com/articles/using-multiple-buildpacks-for-an-app):

~~~bash
heroku buildpacks:add --index 1 heroku/ruby
heroku buildpacks:add --index 2 https://github.com/weibeld/heroku-buildpack-info.git
~~~

You can always check which buildpacks you have currently added to your app with:

~~~bash
heroku buildpacks
~~~


License
-------

Licensed under the MIT License. See [LICENSE.md](LICENSE.md) file.

