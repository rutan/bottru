# Bottru

**This project is in the concept.**

Bottru is chatbot framework for ruby.

## Usage

write `Bottrufile.rb`

```ruby
# Bottrufile.rb

Bottru.configure do
  adapter Bottru::Adapters::Slack do
    config :token, ENV['SLACK_TOKEN']

    input_filter Bottru::Filters::Slack::IgnoreChannel do
      config :channels, %w[general]
    end
  end

  adapter Bottru::Adapters::TailFile, only: :input do
    config :path, './path/to/file'
  end

  adapter Bottru::Adapters::Logger, only: :output do
    config :path, './path/to/log'
  end

  handler Bottru::Handlers::Ping
  handler Bottru::Handlers::RandomNumber do
    config :min, 1
    config :max, 1000
  end

  output_filter -> (message) {
    message.body += "なのー"
    message
  }
end
```

and run bottru

```
$ ls
Bottrufile.rb

$ bottru
```

