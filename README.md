If you run into issues with your ruby or gems, try deleting the `Gemfile.lock`, then running `bundle install` again (you probably have to do this for the first time on a new device).

If you're on Mac, make sure you're *not* using the pre-installed version of ruby. Instead, use ruby from homebrew.

To test locally, run:

```
bundle exec jekyll serve
```

Push to GitHub on the `master` branch to publish.
