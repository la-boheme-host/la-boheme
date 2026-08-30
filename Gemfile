source "https://rubygems.org"

# =========================================================
# Chirpy 테마 및 Jekyll 핵심 Gem 설정
# =========================================================
gem "jekyll", "~> 4.3.0"
gem "jekyll-theme-chirpy", "~> 6.0.0"

# Ruby 3.4+ 버전 호환용 필수 모듈 (LoadError 해결)
gem "csv"
gem "webrick"

# =========================================================
# 필수 플러그인 그룹
# =========================================================
group :jekyll_plugins do
  gem "jekyll-feed"
  gem "jekyll-seo-tag"
  gem "jekyll-sitemap"
  gem "jekyll-paginate"
end

# Windows / Unix 호환성 보장 Gem
platforms :mingw, :x64_mingw, :mswin, :jruby do
  gem "tzinfo", ">= 1.2", "< 3.0"
  gem "tzinfo-data"
end

gem "wdm", "~> 0.1.1", :platforms => [:mingw, :x64_mingw, :mswin]
gem "base64", "~> 0.3.0"
