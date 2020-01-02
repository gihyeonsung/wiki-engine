source "https://rubygems.org"

gem "jekyll", "~> 4.0.0"
gem "therubyracer"
group :jekyll_plugins do
  gem "jekyll-feed", "~> 0.12"
  gem "jekyll-katex"
  gem "jekyll-sitemap"
  gem "jekyll-toc"
end

install_if -> { RUBY_PLATFORM =~ %r!mingw|mswin|java! } do
  gem "tzinfo", "~> 1.2"
  gem "tzinfo-data"
end
