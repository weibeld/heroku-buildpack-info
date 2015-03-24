Heroku Buildpack: Info
======================

Display information about the build process of a Heroku app, i.e. what happens when you do `git push heroku master`.


Description
-----------

This buildpack doesn't do any transformations, it just displays various locations and their contents on the build dyno during the build of your app. It is useful to better understand the build process.

As a **summary**, when you do `git push heroku master`, then:

- your app directory is sent to a **build dyno** where it is placed in a certain directory
- the **slug compiler** running on the build dyno fetches the **buildpack** and executes the `detect`, `compile`, and `release` (if present) scripts
- your app directory, along with any transformations made by the `compile` script, (i.e. the **"slug"**) is loaded as `/app` onto the production **dynos**, and the dynos are started


Usage
-----

Simply do

~~~bash
heroku buildpack:set https://github.com/weibeld/heroku-buildpack-info.git
~~~

On the next `git push heroku master`, the Info buildpack will be used.

For more information on how to use custom buildpacks, see <https://devcenter.heroku.com/articles/third-party-buildpacks#using-a-custom-buildpack>.


Usage together with other buildpacks
------------------------------------

To use multiple buildpacks, you can use [heroku-buildpack-multi](
https://github.com/ddollar/heroku-buildpack-multi):

~~~bash
# Create file .buildpacks in app root, listing the buildpacks you want to use
cat <<EOF >.buildpacks
https://github.com/heroku/heroku-buildpack-ruby.git
https://github.com/weibeld/heroku-buildpack-info.git
EOF

heroku buildpack:set https://github.com/ddollar/heroku-buildpack-multi.git
~~~

On the next `git push heroku master`, all the buildpacks listed in `.buildpacks` will be used.


License
-------

Licensed under the MIT License. See [LICENSE.md](LICENSE.md) file.

