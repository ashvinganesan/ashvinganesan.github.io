# Local Development

Run the site locally to preview changes before deploying.

## Prereqs
- macOS with Homebrew
- Xcode Command Line Tools (`xcode-select --install`)

## Option A: Native (rbenv)
```bash
cd "/Users/ashvin/Documents/personal_website/ashvinganesan.github.io"
brew install rbenv ruby-build
# init rbenv in this shell (bash)
eval "$(rbenv init - bash)"
# install Ruby required by Gemfile
rbenv install -s 3.3.0
rbenv local 3.3.0
ruby -v
# install gems locally
gem install bundler -N
bundle config set path vendor/bundle
bundle config set force_ruby_platform true
bundle install
# serve locally
bundle exec jekyll serve --livereload --host 0.0.0.0 --port 4000
```
Open: http://localhost:4000

## Option B: Docker (no Ruby setup)
```bash
cd "/Users/ashvin/Documents/personal_website/ashvinganesan.github.io"
docker run --rm -it \
  -p 4000:4000 \
  -v "$PWD":/srv/jekyll \
  -v "$PWD/vendor/bundle":/usr/local/bundle \
  jekyll/jekyll:3.9 \
  jekyll serve --livereload --host 0.0.0.0 --port 4000
```

## Common Issues
- Missing CLT: `xcode-select --install`
- Native gem failures: `brew install pkg-config`
- GitHub metadata warnings are safe locally.
- Subdomain redirects (e.g., `games.ashvinganesan.me`) won’t trigger on localhost.
