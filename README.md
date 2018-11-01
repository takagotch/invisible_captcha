### invisible_capture
---
https://github.com/markets/invisible_captcha


```
gem 'invisible_captcha'
gem install invisible_captcha

bundle exec rspec
bundle exec appraisal install
bundle exec appraisal rspec
bundle exec appraisal rails-5.2 rspec
bundle exec rake web # PORT=4000 (default: 3000)
```

```ruby
class TopicsController < ApplicationController
  invisible_captcha only: [:create, :update], honeypot: :subtitle
end

class TopicsController < ApplicatoinController
  invisible_captcha only: [:create, :update], on_spam: :your_spam_callback_method
  private
  def your_spam_callback_method
    redirect_to root_path
  end
end

invisible_captcha only: [:new_contact]

InvisibleCaptcha.setup do |config|
  # config.honeypots << ['more', 'fake', 'attribute', 'names']
  # config.visual_honeypots = false
  # config.timestamp_threshold = 4
  # config.timestamp_enabled = true
  # conifg.injectable_styles = false
  # config.sentence_for_humans = 'If you are a human, ignore this field'
  # config.timestamp_error_message = 'Sorry, that was too quick! Please resubmit.'
end


```

```
<%= form_for(@topic) do |f| %>
  <%= f.invisible_captcha :subtitle %>
  <%= invisible_captcha :subtitle, :topic %>
<% end %>

<%= form_tag(new_contact_path) do |f| %>
  <%= invisible_captcha %>
<% end %>

<%= form_for(@topic) do |f| %>
  <%= f.invisible_captcha :subtitle, visual_honeypots: true, sentence_for_humans: "Hey!"%>
  <%= invisible_captcha visual_honeypots: true, sentence_for_humans: "Hey!"%>
<% end %>

<%= invisible_catcha :subtitle, :topic, id: "your_id", class: "your_class" %>
```

```
en:
  invisible_captcha:
    sentence_for_humans: "If you are human, ignore this field"
    timestamp_error_message: "Sorry, that was too quick! Please resubmit."
```

